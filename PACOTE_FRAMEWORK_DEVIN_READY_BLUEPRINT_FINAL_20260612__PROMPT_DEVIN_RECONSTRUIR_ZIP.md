# Prompt para Devin — Reconstrução fiel do pacote a partir do payload Markdown

## Objetivo

Reconstruir o arquivo `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612.zip` a partir do payload `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612__PAYLOAD_RECONSTRUCAO_INTEGRAL.md` sem alterar, adicionar, remover ou corromper nenhum arquivo interno.

Critério de sucesso obrigatório:

- SHA-256 do `.zip` reconstruído exatamente igual a `69c2ff3fc2dc7f9141f2a839a4cd44d59a7084ad1d92b7c9769126182786bdac`;
- tamanho do `.zip` reconstruído exatamente igual a `140217` bytes;
- contagem de entradas exatamente igual a `74`;
- cada entrada interna com mesmo caminho, mesma ordem, mesmo tamanho e mesmo SHA-256 descritos no payload;
- se qualquer validação falhar, interrompa a tarefa e declare falha.

## Regras absolutas

1. Não copie conteúdo manualmente.
2. Não normalize encoding, acentos, quebras de linha, permissões, timestamps ou caminhos.
3. Não reconstrua o `.zip` por extração e recompactação como caminho principal.
4. Use o bloco `DEVIN_ORIGINAL_ZIP_START`/`DEVIN_ORIGINAL_ZIP_END` do payload para reconstrução byte-a-byte do `.zip`.
5. Use os blocos `DEVIN_ENTRY_START`/`DEVIN_ENTRY_END` para validação granular de todos os arquivos.
6. Não declare sucesso com base em inspeção visual. Sucesso só existe com hash e validação programática.
7. Não altere o payload Markdown.

## Arquivos esperados

- Payload de entrada: `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612__PAYLOAD_RECONSTRUCAO_INTEGRAL.md`
- ZIP de saída: `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612.zip`
- Raiz interna esperada no ZIP: `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/`

## Procedimento obrigatório

Crie o script abaixo em `tools/reconstruct_devin_package_from_payload.py` e execute-o no repositório.

```bash
mkdir -p tools
python3 tools/reconstruct_devin_package_from_payload.py \
  --payload "PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612__PAYLOAD_RECONSTRUCAO_INTEGRAL.md" \
  --out-dir "." \
  --extract-verify
```

Se o `.zip` de saída já existir e tiver SHA-256 diferente do esperado, o script irá falhar por segurança. Nesse caso, investigue a divergência; não sobrescreva silenciosamente.

## Script obrigatório

```python
#!/usr/bin/env python3
from __future__ import annotations

import argparse
import base64
import hashlib
import json
import os
import pathlib
import re
import shutil
import sys
import zipfile


EXPECTED_ZIP_NAME = "PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612.zip"
EXPECTED_ZIP_SHA256 = "69c2ff3fc2dc7f9141f2a839a4cd44d59a7084ad1d92b7c9769126182786bdac"
EXPECTED_ZIP_SIZE_BYTES = 140217
EXPECTED_ENTRY_COUNT = 74

ORIGINAL_ZIP_RE = re.compile(
    r"<!-- DEVIN_ORIGINAL_ZIP_START (?P<meta>\{.*?\}) -->\s*"
    r"```base64-zip\s*(?P<data>.*?)\s*```\s*"
    r"<!-- DEVIN_ORIGINAL_ZIP_END (?P<end>\{.*?\}) -->",
    re.S,
)

ENTRY_RE = re.compile(
    r"<!-- DEVIN_ENTRY_START (?P<meta>\{.*?\}) -->\s*"
    r"```base64\s*(?P<data>.*?)\s*```\s*"
    r"<!-- DEVIN_ENTRY_END (?P<end>\{.*?\}) -->",
    re.S,
)


def sha256_bytes(data: bytes) -> str:
    return hashlib.sha256(data).hexdigest()


def fail(message: str) -> None:
    raise SystemExit(f"[FALHA] {message}")


def decode_base64_block(raw: str) -> bytes:
    compact = "".join(raw.split())
    try:
        return base64.b64decode(compact, validate=True)
    except Exception as exc:
        fail(f"base64 inválido: {exc}")
        raise AssertionError("unreachable")


def ensure_safe_relative_zip_path(path: str) -> None:
    # ZIP usa caminhos POSIX. Impedir path traversal e caminhos absolutos.
    pure = pathlib.PurePosixPath(path)
    if path.startswith("/") or path.startswith("\\"):
        fail(f"caminho absoluto proibido no ZIP: {path!r}")
    if any(part in ("", ".", "..") for part in pure.parts):
        fail(f"caminho inseguro no ZIP: {path!r}")


def parse_original_zip(text: str) -> tuple[dict, bytes]:
    match = ORIGINAL_ZIP_RE.search(text)
    if not match:
        fail("bloco DEVIN_ORIGINAL_ZIP_START/END não encontrado")
    meta = json.loads(match.group("meta"))
    end_meta = json.loads(match.group("end"))
    zip_bytes = decode_base64_block(match.group("data"))

    if meta.get("zip_name") != EXPECTED_ZIP_NAME:
        fail(f"nome do ZIP divergente no payload: {meta.get('zip_name')}")
    if end_meta.get("sha256") != meta.get("sha256"):
        fail("SHA-256 do início/fim do bloco ZIP não bate")
    if len(zip_bytes) != int(meta.get("size_bytes")):
        fail("tamanho do ZIP decodificado não bate com o payload")
    if sha256_bytes(zip_bytes) != meta.get("sha256"):
        fail("SHA-256 do ZIP decodificado não bate com o payload")
    if sha256_bytes(zip_bytes) != EXPECTED_ZIP_SHA256:
        fail("SHA-256 do ZIP decodificado não bate com o esperado externo")
    if len(zip_bytes) != EXPECTED_ZIP_SIZE_BYTES:
        fail("tamanho do ZIP decodificado não bate com o esperado externo")

    return meta, zip_bytes


def parse_entries(text: str) -> list[tuple[dict, bytes]]:
    entries: list[tuple[dict, bytes]] = []
    for match in ENTRY_RE.finditer(text):
        meta = json.loads(match.group("meta"))
        end_meta = json.loads(match.group("end"))
        data = decode_base64_block(match.group("data"))

        for key in ("index", "path", "sha256", "size_bytes", "type"):
            if end_meta.get(key) != meta.get(key):
                fail(f"metadado divergente entre início/fim da entrada {meta.get('index')}: {key}")

        ensure_safe_relative_zip_path(meta["path"])

        if len(data) != int(meta["size_bytes"]):
            fail(f"tamanho divergente na entrada {meta['path']}")
        if sha256_bytes(data) != meta["sha256"]:
            fail(f"SHA-256 divergente na entrada {meta['path']}")
        if meta["type"] not in ("file", "directory"):
            fail(f"tipo inválido na entrada {meta['path']}: {meta['type']}")

        entries.append((meta, data))

    if len(entries) != EXPECTED_ENTRY_COUNT:
        fail(f"contagem de entradas divergente: {len(entries)} != {EXPECTED_ENTRY_COUNT}")

    for expected_index, (meta, _data) in enumerate(entries):
        if int(meta["index"]) != expected_index:
            fail(f"índice fora de ordem: esperado {expected_index}, encontrado {meta['index']}")

    return entries


def verify_zip_against_entries(zip_path: pathlib.Path, entries: list[tuple[dict, bytes]]) -> None:
    if not zip_path.exists():
        fail(f"ZIP não encontrado para validação: {zip_path}")

    actual_bytes = zip_path.read_bytes()
    if len(actual_bytes) != EXPECTED_ZIP_SIZE_BYTES:
        fail("tamanho do ZIP final divergente")
    if sha256_bytes(actual_bytes) != EXPECTED_ZIP_SHA256:
        fail("SHA-256 do ZIP final divergente")

    with zipfile.ZipFile(zip_path, "r") as zf:
        infos = zf.infolist()
        if len(infos) != len(entries):
            fail(f"contagem de entradas no ZIP final divergente: {len(infos)} != {len(entries)}")

        zip_names = [info.filename for info in infos]
        expected_names = [meta["path"] for meta, _data in entries]
        if zip_names != expected_names:
            fail("ordem/caminhos das entradas no ZIP final divergem do payload")

        for info, (meta, expected_data) in zip(infos, entries):
            ensure_safe_relative_zip_path(info.filename)
            expected_type = meta["type"]
            actual_type = "directory" if info.is_dir() else "file"
            if actual_type != expected_type:
                fail(f"tipo divergente em {info.filename}: {actual_type} != {expected_type}")

            if info.file_size != int(meta["size_bytes"]):
                fail(f"tamanho declarado pelo ZIP diverge em {info.filename}")

            if info.is_dir():
                actual_data = b""
            else:
                with zf.open(info, "r") as fh:
                    actual_data = fh.read()

            if actual_data != expected_data:
                fail(f"bytes do arquivo divergem em {info.filename}")
            if sha256_bytes(actual_data) != meta["sha256"]:
                fail(f"SHA-256 interno diverge em {info.filename}")

    print("[OK] ZIP final validado contra SHA-256 global e contra todas as entradas internas.")


def safe_extract_for_verification(zip_path: pathlib.Path, extract_root: pathlib.Path) -> None:
    if extract_root.exists():
        shutil.rmtree(extract_root)
    extract_root.mkdir(parents=True, exist_ok=False)
    root_resolved = extract_root.resolve()

    with zipfile.ZipFile(zip_path, "r") as zf:
        for info in zf.infolist():
            ensure_safe_relative_zip_path(info.filename)
            target = extract_root / pathlib.PurePosixPath(info.filename)
            target_resolved = target.resolve()
            if os.path.commonpath([str(root_resolved), str(target_resolved)]) != str(root_resolved):
                fail(f"path traversal detectado durante extração: {info.filename}")

            if info.is_dir():
                target.mkdir(parents=True, exist_ok=True)
                continue

            target.parent.mkdir(parents=True, exist_ok=True)
            with zf.open(info, "r") as src, open(target, "wb") as dst:
                shutil.copyfileobj(src, dst)

    print(f"[OK] Extração de verificação criada em: {extract_root}")


def main() -> int:
    parser = argparse.ArgumentParser()
    parser.add_argument("--payload", required=True, help="Markdown com payload integral")
    parser.add_argument("--out-dir", required=True, help="Diretório onde gravar o ZIP reconstruído")
    parser.add_argument("--extract-verify", action="store_true", help="Extrair ZIP para pasta temporária de validação")
    args = parser.parse_args()

    payload_path = pathlib.Path(args.payload)
    out_dir = pathlib.Path(args.out_dir)
    out_dir.mkdir(parents=True, exist_ok=True)

    if not payload_path.exists():
        fail(f"payload não encontrado: {payload_path}")

    text = payload_path.read_text(encoding="utf-8")
    _zip_meta, zip_bytes = parse_original_zip(text)
    entries = parse_entries(text)

    out_zip = out_dir / EXPECTED_ZIP_NAME
    if out_zip.exists():
        existing_sha = sha256_bytes(out_zip.read_bytes())
        if existing_sha != EXPECTED_ZIP_SHA256:
            fail(
                f"já existe um ZIP com nome esperado, mas SHA-256 divergente: {out_zip} "
                f"({existing_sha} != {EXPECTED_ZIP_SHA256}). Não sobrescrevendo silenciosamente."
            )
        print(f"[OK] ZIP já existia e já estava correto: {out_zip}")
    else:
        out_zip.write_bytes(zip_bytes)
        print(f"[OK] ZIP reconstruído: {out_zip}")

    verify_zip_against_entries(out_zip, entries)

    if args.extract_verify:
        safe_extract_for_verification(out_zip, out_dir / "_devin_reconstruction_extract_verify")

    print("[SUCESSO] Reconstrução concluída sem divergências.")
    print(f"[SUCESSO] ZIP: {out_zip}")
    print(f"[SUCESSO] SHA-256: {EXPECTED_ZIP_SHA256}")
    return 0


if __name__ == "__main__":
    raise SystemExit(main())
```

## Saída esperada

Ao final, reporte exatamente:

- caminho do `.zip` reconstruído;
- SHA-256 do `.zip`;
- número de entradas validadas;
- confirmação de que a extração de verificação foi feita;
- qualquer divergência encontrada, caso exista.

Não inicie implementação baseada nesses documentos até a reconstrução passar integralmente.
