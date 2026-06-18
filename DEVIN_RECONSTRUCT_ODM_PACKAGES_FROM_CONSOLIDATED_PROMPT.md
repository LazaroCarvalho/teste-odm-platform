# Prompt para Devin — Reconstrução segura dos pacotes ODM a partir do Markdown consolidado

## Modo da sessão

Você está em modo **reconstrução byte-safe / fail-closed**.

Sua tarefa é receber o arquivo consolidado `ODM_DUAL_PACKAGE_CONSOLIDATED_BYTE_SAFE.md` e reconstruir os dois pacotes ZIP originais sem modificar, normalizar ou reinterpretar o conteúdo.

## Entrada obrigatória

- Arquivo consolidado: `ODM_DUAL_PACKAGE_CONSOLIDATED_BYTE_SAFE.md`
- SHA-256 esperado do arquivo consolidado: `1929fcdd3bd753fe538f428d0ff11646b204380d9dddab282e61fc7b6e9f2be7`

## Pacotes que devem ser reconstruídos

- `ODM_CHATGPT_OPTIMIZED_SUPPORT_PACK_CONSOLIDATED.zip` — SHA-256 `e9be726913c9c5fbc64841a47c54cd46261ac64e53f0856faaa5a093a9a9cfaa`, 44052 bytes, 13 arquivos.
- `ODM_V7_TARGET_ARCHITECTURE_CONSOLIDATED_FINAL.zip` — SHA-256 `fcff16d7910c01c7b1e4d2897ee9d0c8fa2165b6e00f74539e7c734553f4eba6`, 769940 bytes, 192 arquivos.

## Regras não negociáveis

1. **Não edite o `.md` consolidado.** Trate-o como artefato imutável.
2. **Não altere nem sobrescreva os ZIPs originais**, se eles também existirem no repositório.
3. Trabalhe sempre em uma pasta nova, por exemplo `reconstruction_out/`.
4. O processo deve ser **fail-closed**: qualquer divergência de SHA-256, tamanho, contagem, Base64 inválido ou caminho inseguro deve abortar a reconstrução.
5. Para reconstrução exata dos ZIPs, use somente os blocos `ODM_ZIP_BINARY_BEGIN/END`.
6. Para auditoria por arquivo, use somente os blocos `ODM_FILE_BASE64_BEGIN/END`.
7. Nunca use as seções `ODM_FILE_TEXT_BEGIN/END` para reconstrução. Elas são apenas leitura humana e podem não preservar byte final visualmente.
8. Não faça “correções” automáticas de encoding, newline, normalização Unicode, separador de caminho, ordenação, compressão ou conteúdo.
9. Não declare sucesso se qualquer validação falhar.
10. O sucesso exige relatório final com hashes calculados e confirmação explícita de que os hashes batem com os esperados.

## Estratégia correta

### Caminho A — reconstrução exata dos ZIPs originais

1. Calcular SHA-256 do arquivo `ODM_DUAL_PACKAGE_CONSOLIDATED_BYTE_SAFE.md` e comparar com `1929fcdd3bd753fe538f428d0ff11646b204380d9dddab282e61fc7b6e9f2be7`.
2. Localizar todos os blocos:
   - `<!-- ODM_ZIP_BINARY_BEGIN {...} -->`
   - bloco fenced `base64`
   - `<!-- ODM_ZIP_BINARY_END {...} -->`
3. Decodificar o Base64 com validação estrita.
4. Validar `zip_size_bytes` e `zip_sha256` de cada pacote.
5. Escrever os ZIPs reconstruídos em `reconstruction_out/exact_zips/` usando exatamente o nome `package_name` do metadado.
6. Recalcular SHA-256 dos ZIPs escritos e comparar com o manifest.
7. Abrir cada ZIP com ferramenta padrão e executar teste de integridade.

### Caminho B — auditoria file-by-file

1. Localizar todos os blocos `ODM_FILE_BEGIN/END`.
2. Dentro de cada bloco, use apenas `ODM_FILE_BASE64_BEGIN/END`.
3. Decodificar cada payload Base64.
4. Validar `size_bytes` e `sha256` por arquivo.
5. Escrever cada arquivo em `reconstruction_out/file_trees/<package_id>/`, preservando `entry_path` exatamente como caminho POSIX relativo.
6. Validar proteção contra Zip Slip/path traversal:
   - rejeitar caminho absoluto;
   - rejeitar `..`;
   - rejeitar backslash `\`;
   - rejeitar NUL;
   - rejeitar drive Windows como `C:`.
7. Gerar relatório de inventário por pacote.
8. Opcionalmente, criar ZIPs normalizados a partir das árvores auditadas, mas **não comparar o SHA do ZIP normalizado com o SHA do ZIP original**, pois metadados de container/compressão podem mudar. A comparação canônica file-by-file é por caminho, tamanho e SHA-256 do conteúdo.

## Script recomendado

Crie e execute um arquivo `reconstruct_odm_packages_from_md.py` com o conteúdo abaixo.

````python
from __future__ import annotations

import base64
import hashlib
import json
import os
import re
import sys
import zipfile
from pathlib import Path, PurePosixPath

CONSOLIDATED_MD = Path("ODM_DUAL_PACKAGE_CONSOLIDATED_BYTE_SAFE.md")
EXPECTED_MD_SHA256 = "1929fcdd3bd753fe538f428d0ff11646b204380d9dddab282e61fc7b6e9f2be7"
OUT_DIR = Path("reconstruction_out")
EXACT_ZIP_DIR = OUT_DIR / "exact_zips"
FILE_TREE_DIR = OUT_DIR / "file_trees"
REPORT_PATH = OUT_DIR / "RECONSTRUCTION_REPORT.md"

ZIP_SECTION_RE = re.compile(
    r'^<!-- ODM_ZIP_BINARY_BEGIN (?P<meta>\{.*?\}) -->\n```base64\n(?P<b64>.*?)\n```\n<!-- ODM_ZIP_BINARY_END (?P<endmeta>\{.*?\}) -->$',
    re.M | re.S,
)

FILE_SECTION_RE = re.compile(
    r'^<!-- ODM_FILE_BEGIN (?P<meta>\{.*?\}) -->.*?^<!-- ODM_FILE_BASE64_BEGIN (?P<b64meta>\{.*?\}) -->\n```base64\n(?P<b64>.*?)\n```\n<!-- ODM_FILE_BASE64_END (?P<b64end>\{.*?\}) -->.*?^<!-- ODM_FILE_END (?P<endmeta>\{.*?\}) -->$',
    re.M | re.S,
)


def sha256_bytes(data: bytes) -> str:
    return hashlib.sha256(data).hexdigest()


def sha256_file(path: Path) -> str:
    h = hashlib.sha256()
    with path.open("rb") as f:
        for chunk in iter(lambda: f.read(1024 * 1024), b""):
            h.update(chunk)
    return h.hexdigest()


def decode_b64_strict(payload: str) -> bytes:
    compact = "".join(payload.split())
    return base64.b64decode(compact, validate=True)


def reject_unsafe_zip_name(name: str) -> None:
    if name != os.path.basename(name):
        raise ValueError(f"Unsafe package_name: {name!r}")
    if "\x00" in name or not name.endswith(".zip"):
        raise ValueError(f"Invalid package_name: {name!r}")


def safe_output_path(root: Path, entry_path: str) -> Path:
    if "\x00" in entry_path:
        raise ValueError(f"NUL in path: {entry_path!r}")
    if "\\" in entry_path:
        raise ValueError(f"Backslash in POSIX zip path: {entry_path!r}")
    if re.match(r"^[A-Za-z]:", entry_path):
        raise ValueError(f"Windows drive path rejected: {entry_path!r}")
    posix = PurePosixPath(entry_path)
    if posix.is_absolute() or any(part == ".." for part in posix.parts):
        raise ValueError(f"Path traversal rejected: {entry_path!r}")
    out = root.joinpath(*posix.parts)
    resolved_root = root.resolve()
    resolved_parent = out.parent.resolve()
    if resolved_root not in (resolved_parent, *resolved_parent.parents):
        raise ValueError(f"Resolved path escapes root: {entry_path!r}")
    return out


def hard_fail(message: str) -> None:
    print(f"BLOCKER: {message}", file=sys.stderr)
    sys.exit(1)


def main() -> None:
    if not CONSOLIDATED_MD.exists():
        hard_fail(f"Input file not found: {CONSOLIDATED_MD}")

    md_bytes = CONSOLIDATED_MD.read_bytes()
    actual_md_sha = sha256_bytes(md_bytes)
    if actual_md_sha != EXPECTED_MD_SHA256:
        hard_fail(f"Consolidated MD SHA mismatch: expected {EXPECTED_MD_SHA256}, got {actual_md_sha}")

    if OUT_DIR.exists():
        hard_fail(f"Output dir already exists. Remove it manually after review: {OUT_DIR}")
    EXACT_ZIP_DIR.mkdir(parents=True)
    FILE_TREE_DIR.mkdir(parents=True)

    text = md_bytes.decode("utf-8")
    report_lines = []
    report_lines.append("# RECONSTRUCTION_REPORT")
    report_lines.append("")
    report_lines.append(f"Consolidated MD SHA-256: `{actual_md_sha}`")
    report_lines.append("")

    zip_matches = list(ZIP_SECTION_RE.finditer(text))
    if not zip_matches:
        hard_fail("No ODM_ZIP_BINARY sections found")

    report_lines.append("## Exact ZIP reconstruction")
    report_lines.append("")
    report_lines.append("| package_id | package_name | expected_sha256 | actual_sha256 | size_bytes | zip_test |")
    report_lines.append("|---|---|---|---|---:|---|")

    package_file_counts = {}
    for match in zip_matches:
        meta = json.loads(match.group("meta"))
        endmeta = json.loads(match.group("endmeta"))
        if meta.get("package_id") != endmeta.get("package_id"):
            hard_fail(f"ZIP metadata mismatch: {meta} vs {endmeta}")
        package_name = meta["package_name"]
        reject_unsafe_zip_name(package_name)
        data = decode_b64_strict(match.group("b64"))
        expected_size = int(meta["zip_size_bytes"])
        expected_sha = meta["zip_sha256"]
        actual_sha = sha256_bytes(data)
        if len(data) != expected_size:
            hard_fail(f"ZIP size mismatch for {package_name}")
        if actual_sha != expected_sha:
            hard_fail(f"ZIP SHA mismatch for {package_name}")
        out_path = EXACT_ZIP_DIR / package_name
        out_path.write_bytes(data)
        if sha256_file(out_path) != expected_sha:
            hard_fail(f"Written ZIP SHA mismatch for {package_name}")
        with zipfile.ZipFile(out_path, "r") as zf:
            bad = zf.testzip()
            if bad is not None:
                hard_fail(f"ZIP test failed for {package_name} at {bad}")
        package_file_counts[meta["package_id"]] = int(meta["file_count"])
        report_lines.append(f"| {meta['package_id']} | `{package_name}` | `{expected_sha}` | `{actual_sha}` | {len(data)} | OK |")

    file_matches = list(FILE_SECTION_RE.finditer(text))
    if not file_matches:
        hard_fail("No ODM_FILE sections found")

    report_lines.append("")
    report_lines.append("## File-by-file audit")
    report_lines.append("")
    counts_by_package = {}
    bytes_by_package = {}

    seen_full_paths = set()
    for match in file_matches:
        meta = json.loads(match.group("meta"))
        b64meta = json.loads(match.group("b64meta"))
        b64end = json.loads(match.group("b64end"))
        endmeta = json.loads(match.group("endmeta"))
        for k in ["package_id", "entry_path", "full_path", "sha256"]:
            if str(meta.get(k)) != str(endmeta.get(k)):
                hard_fail(f"FILE metadata mismatch for key {k}: {meta} vs {endmeta}")
        if meta["full_path"] in seen_full_paths:
            hard_fail(f"Duplicate full_path: {meta['full_path']}")
        seen_full_paths.add(meta["full_path"])
        if b64meta.get("sha256") != meta.get("sha256") or b64end.get("sha256") != meta.get("sha256"):
            hard_fail(f"Base64 metadata SHA mismatch for {meta['full_path']}")
        data = decode_b64_strict(match.group("b64"))
        if len(data) != int(meta["size_bytes"]):
            hard_fail(f"File size mismatch for {meta['full_path']}")
        if sha256_bytes(data) != meta["sha256"]:
            hard_fail(f"File SHA mismatch for {meta['full_path']}")
        pkg_root = FILE_TREE_DIR / meta["package_id"]
        out_path = safe_output_path(pkg_root, meta["entry_path"])
        out_path.parent.mkdir(parents=True, exist_ok=True)
        out_path.write_bytes(data)
        if sha256_file(out_path) != meta["sha256"]:
            hard_fail(f"Written file SHA mismatch for {meta['full_path']}")
        counts_by_package[meta["package_id"]] = counts_by_package.get(meta["package_id"], 0) + 1
        bytes_by_package[meta["package_id"]] = bytes_by_package.get(meta["package_id"], 0) + len(data)

    for package_id, expected_count in sorted(package_file_counts.items()):
        actual_count = counts_by_package.get(package_id, 0)
        if actual_count != expected_count:
            hard_fail(f"File count mismatch for {package_id}: expected {expected_count}, got {actual_count}")

    report_lines.append("| package_id | file_count | total_file_bytes | status |")
    report_lines.append("|---|---:|---:|---|")
    for package_id in sorted(counts_by_package):
        report_lines.append(f"| {package_id} | {counts_by_package[package_id]} | {bytes_by_package[package_id]} | OK |")

    report_lines.append("")
    report_lines.append("## Resultado")
    report_lines.append("")
    report_lines.append("GO — reconstrução exata dos ZIPs e auditoria file-by-file concluídas com hashes válidos.")
    REPORT_PATH.write_text("\n".join(report_lines) + "\n", encoding="utf-8")
    print(f"GO: reconstructed {len(zip_matches)} exact ZIPs and audited {len(file_matches)} files.")
    print(f"Report: {REPORT_PATH}")


if __name__ == "__main__":
    main()
````

## Entregáveis esperados do Devin

Ao finalizar, entregue:

1. `reconstruction_out/exact_zips/ODM_CHATGPT_OPTIMIZED_SUPPORT_PACK_CONSOLIDATED.zip`
2. `reconstruction_out/exact_zips/ODM_V7_TARGET_ARCHITECTURE_CONSOLIDATED_FINAL.zip`
3. `reconstruction_out/file_trees/PKG001/` com os arquivos auditados do pacote de suporte ChatGPT.
4. `reconstruction_out/file_trees/PKG002/` com os arquivos auditados da documentação arquitetural target.
5. `reconstruction_out/RECONSTRUCTION_REPORT.md`

## Critério de GO / NO-GO

### GO

Declare `GO` somente se:

- o SHA-256 do `.md` consolidado bater com `1929fcdd3bd753fe538f428d0ff11646b204380d9dddab282e61fc7b6e9f2be7`;
- os dois ZIPs forem reconstruídos a partir dos blocos `ODM_ZIP_BINARY`;
- os SHA-256 dos dois ZIPs reconstruídos baterem com o manifest;
- `zipfile.testzip()` passar para ambos os ZIPs;
- todos os arquivos dos blocos `ODM_FILE_BASE64` forem decodificados;
- todos os arquivos passarem em validação de caminho, tamanho e SHA-256;
- as contagens por pacote baterem.

### NO-GO

Declare `NO-GO` e pare imediatamente se houver:

- hash divergente;
- Base64 inválido;
- arquivo faltante;
- caminho inseguro;
- contagem divergente;
- tentativa de sobrescrever artefato original;
- qualquer necessidade de inferência ou “correção manual”.

## Observação final obrigatória

Não prometa equivalência por inspeção visual. A evidência de integridade aqui é exclusivamente criptográfica e operacional: SHA-256, tamanho, contagem, teste do ZIP e validação file-by-file.
