# Prompt para Devin — Reconstituir ZIP a partir do Markdown unificado

Você receberá o arquivo:

`PACOTE_A7_UNIFICADO_RECONSTRUIVEL_DEVIN.md`

Ele contém o pacote original `PACOTE_REBASE_FINAL_DEVIN_READY_v5_A7_PACOTE_CORRIGIDO_LEDGER_HANDOFF.zip` serializado em Markdown, com duas formas de reconstrução:

1. **Reconstrução primária byte-a-byte**, usando o bloco `BEGIN_ORIGINAL_ZIP_BASE64` / `END_ORIGINAL_ZIP_BASE64`.
2. **Reconstrução alternativa por arquivos internos**, usando blocos `BEGIN_ZIP_ENTRY` / `END_ZIP_ENTRY`.

## Objetivo obrigatório

Reconstruir o arquivo ZIP original e validar que ele é íntegro antes de usá-lo.

## SHA-256 esperado do ZIP original

```text
d8248ce8d2c181db1ab3bc8f4fa226cc8b3176be988e2320368d5e1e6a42e00c
```

## Procedimento obrigatório — caminho primário

1. Abra o Markdown recebido.
2. Localize exatamente o bloco delimitado por:

```text
BEGIN_ORIGINAL_ZIP_BASE64
END_ORIGINAL_ZIP_BASE64
```

3. Extraia somente o conteúdo Base64 dentro do code fence desse bloco.
4. Remova quebras de linha e espaços.
5. Decodifique o Base64 para bytes.
6. Grave os bytes com o nome:

```text
PACOTE_REBASE_FINAL_DEVIN_READY_v5_A7_PACOTE_CORRIGIDO_LEDGER_HANDOFF.zip
```

7. Calcule o SHA-256 do ZIP reconstruído.
8. Compare com o hash esperado:

```text
d8248ce8d2c181db1ab3bc8f4fa226cc8b3176be988e2320368d5e1e6a42e00c
```

9. Execute teste de integridade do ZIP.
10. Se o SHA-256 bater e o ZIP abrir sem erro, considere a reconstrução concluída.

## Script Python recomendado

Use este script como referência segura:

```python
from pathlib import Path
import base64
import hashlib
import re
import zipfile

md_path = Path("PACOTE_A7_UNIFICADO_RECONSTRUIVEL_DEVIN.md")
out_zip = Path("PACOTE_REBASE_FINAL_DEVIN_READY_v5_A7_PACOTE_CORRIGIDO_LEDGER_HANDOFF.zip")
expected_sha256 = "d8248ce8d2c181db1ab3bc8f4fa226cc8b3176be988e2320368d5e1e6a42e00c"

text = md_path.read_text(encoding="utf-8")

match = re.search(
    r"<!-- BEGIN_ORIGINAL_ZIP_BASE64[^>]*-->\s*```base64\s*(.*?)\s*```\s*<!-- END_ORIGINAL_ZIP_BASE64[^>]*-->",
    text,
    flags=re.DOTALL,
)
if not match:
    raise SystemExit("Bloco ORIGINAL_ZIP_BASE64 não encontrado.")

b64 = "".join(match.group(1).split())
zip_bytes = base64.b64decode(b64, validate=True)
out_zip.write_bytes(zip_bytes)

actual_sha256 = hashlib.sha256(zip_bytes).hexdigest()
if actual_sha256 != expected_sha256:
    raise SystemExit(f"SHA-256 divergente: {actual_sha256} != {expected_sha256}")

with zipfile.ZipFile(out_zip, "r") as zf:
    bad = zf.testzip()
    if bad is not None:
        raise SystemExit(f"ZIP corrompido na entrada: {bad}")

print(f"OK: ZIP reconstruído e validado: {out_zip}")
print(f"SHA-256: {actual_sha256}")
```

## Caminho alternativo — somente se o caminho primário for bloqueado

Se não for permitido reconstruir pelo bloco do ZIP inteiro:

1. Percorra todos os blocos `BEGIN_ZIP_ENTRY` / `END_ZIP_ENTRY`.
2. Para cada entrada `DIR`, crie o diretório correspondente.
3. Para cada entrada `FILE`, extraia o conteúdo entre `BEGIN_ENTRY_DATA_BASE64` / `END_ENTRY_DATA_BASE64`.
4. Decodifique o Base64 e grave exatamente no caminho informado no campo `path`.
5. Calcule SHA-256 de cada arquivo e compare com o campo `sha256` da entrada.
6. Só depois gere um novo ZIP funcional.
7. Registre que esse ZIP alternativo pode não ser byte-a-byte idêntico ao ZIP original, porque metadados internos de ZIP, ordem, timestamps e compressão podem variar. A validação principal nesse caminho é o SHA-256 de cada arquivo interno.

## Proibições

- Não editar o conteúdo dos arquivos antes de validar os hashes.
- Não normalizar quebras de linha dos arquivos internos.
- Não converter encoding dos arquivos internos.
- Não renomear caminhos.
- Não remover arquivos aparentemente redundantes.
- Não promover nenhum conteúdo do pacote a norma sem seguir os gates documentais do próprio pacote.

## Resultado esperado

Entregue:

1. ZIP reconstruído.
2. SHA-256 calculado.
3. Resultado do teste de integridade.
4. Lista de eventuais divergências, se existirem.
5. Confirmação explícita de que o pacote reconstruído permanece em estado `FINAL_GO_WITH_WARNINGS`, não `FINAL_GO`, salvo se houver decisão humana posterior registrada.
