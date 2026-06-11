# Prompt para Devin — Reconstruir ZIP original a partir de Markdown consolidado íntegro

Você receberá no repositório ou em anexo o arquivo:

`plano_implementacao_devin_ai_agent_os_v2_1_CONSOLIDADO_INTEGRO.md`

Objetivo: reconstruir com máxima integridade o ZIP original:

`plano_implementacao_devin_ai_agent_os_v2_1.zip`

O Markdown consolidado contém:

1. Um manifesto global com SHA-256 e tamanho do ZIP original.
2. Um bloco autoritativo `ORIGINAL_ZIP_BASE64`, que representa o ZIP original byte-a-byte.
3. Seções por arquivo com `FILE_BEGIN` / `FILE_END`, caminho original, tamanho, SHA-256, `FILE_BASE64` e pré-visualização UTF-8.

## Regras obrigatórias

1. Não editar, normalizar, reformatar, traduzir, copiar manualmente nem reescrever o conteúdo dos arquivos.
2. Não usar os blocos `UTF8_PREVIEW` para reconstrução primária. Eles existem apenas para inspeção humana.
3. Para recuperar o ZIP original com garantia byte-a-byte, usar exclusivamente o bloco `ORIGINAL_ZIP_BASE64`.
4. Validar o SHA-256 do ZIP reconstruído contra:

```text
1d3aad53a318c0dcdd8e1264055c0cef906fbe6bab61dc5ca03b44da7c601317
```

5. Somente depois de validar o SHA-256 do ZIP, extrair seu conteúdo para o repositório.
6. Se o SHA-256 do ZIP reconstruído não bater, parar imediatamente e reportar `NO_GO_INTEGRITY_FAILURE`.
7. Não criar arquivos adicionais dentro da árvore reconstruída.
8. Não remover arquivos existentes fora do diretório alvo sem autorização explícita.
9. Não prosseguir para implementação Devin antes da validação de integridade.

## Procedimento recomendado

Execute em uma área temporária limpa.

### Etapa 1 — Localizar o Markdown consolidado

Localize o arquivo:

```text
plano_implementacao_devin_ai_agent_os_v2_1_CONSOLIDADO_INTEGRO.md
```

Confirme que ele contém os marcadores:

```text
@@@AI_AGENT_OS_V2_1_INTEGRITY_TRANSFER_8F7B3C2D_ORIGINAL_ZIP_BASE64_BEGIN@@@
@@@AI_AGENT_OS_V2_1_INTEGRITY_TRANSFER_8F7B3C2D_ORIGINAL_ZIP_BASE64_END@@@
```

### Etapa 2 — Recriar o ZIP original por Base64

Use o script abaixo, sem alterar os marcadores nem o hash esperado:

```python
from pathlib import Path
import base64
import hashlib
import re
import zipfile
import shutil

md_path = Path("plano_implementacao_devin_ai_agent_os_v2_1_CONSOLIDADO_INTEGRO.md")
out_zip = Path("plano_implementacao_devin_ai_agent_os_v2_1.zip")
expected_sha256 = "1d3aad53a318c0dcdd8e1264055c0cef906fbe6bab61dc5ca03b44da7c601317"
expected_size = 105625

text = md_path.read_text(encoding="utf-8")
pattern = re.compile(
    r"@@@AI_AGENT_OS_V2_1_INTEGRITY_TRANSFER_8F7B3C2D_ORIGINAL_ZIP_BASE64_BEGIN@@@\n(.*?)\n@@@AI_AGENT_OS_V2_1_INTEGRITY_TRANSFER_8F7B3C2D_ORIGINAL_ZIP_BASE64_END@@@",
    re.DOTALL,
)
match = pattern.search(text)
if not match:
    raise SystemExit("NO_GO_INTEGRITY_FAILURE: bloco ORIGINAL_ZIP_BASE64 não encontrado")

payload = "".join(match.group(1).split())
zip_bytes = base64.b64decode(payload, validate=True)
actual_sha256 = hashlib.sha256(zip_bytes).hexdigest()
actual_size = len(zip_bytes)

if actual_sha256 != expected_sha256:
    raise SystemExit(f"NO_GO_INTEGRITY_FAILURE: SHA-256 divergente: {actual_sha256} != {expected_sha256}")
if actual_size != expected_size:
    raise SystemExit(f"NO_GO_INTEGRITY_FAILURE: tamanho divergente: {actual_size} != {expected_size}")

out_zip.write_bytes(zip_bytes)

with zipfile.ZipFile(out_zip, "r") as z:
    bad = z.testzip()
    if bad is not None:
        raise SystemExit(f"NO_GO_INTEGRITY_FAILURE: entrada corrompida no ZIP: {bad}")
    print("ZIP_OK", out_zip, actual_size, actual_sha256)
```

### Etapa 3 — Extrair o ZIP validado

Depois que o script imprimir `ZIP_OK`, extraia o ZIP para o diretório escolhido do repositório. Exemplo:

```python
from pathlib import Path
import zipfile
import shutil

out_zip = Path("plano_implementacao_devin_ai_agent_os_v2_1.zip")
extract_dir = Path(".")

with zipfile.ZipFile(out_zip, "r") as z:
    z.extractall(extract_dir)

print("EXTRACTED_OK", extract_dir.resolve())
```

### Etapa 4 — Validar árvore extraída por arquivo

Após a extração, valide pelo menos:

- número total de arquivos Markdown: `45`;
- presença do diretório raiz `plano_implementacao_devin_ai_agent_os_v2/`;
- presença de `plano_implementacao_devin_ai_agent_os_v2/75_DEVIN_ORCHESTRATION/MASTER_DEVIN_ORCHESTRATION_GUIDE.md`;
- presença de `plano_implementacao_devin_ai_agent_os_v2/00_CONTROLE/HANDOFF_FINAL_PARA_DEVIN_IMPLEMENTACAO.md`;
- presença de `plano_implementacao_devin_ai_agent_os_v2/00_AUDITORIA_FINAL_EXAUSTIVA/INVENTARIO_DOCUMENTAL_COMPLETO.md`.

Opcionalmente, parseie os blocos `FILE_BASE64` do Markdown e compare o SHA-256 de cada arquivo extraído com o SHA-256 informado no respectivo `FILE_BEGIN`.

## Resultado esperado

Ao final, reporte:

```text
PASS_RECONSTRUCTION_INTEGRITY_VERIFIED
```

Inclua no relatório:

- caminho do Markdown consolidado usado;
- caminho do ZIP reconstruído;
- SHA-256 do ZIP reconstruído;
- total de arquivos extraídos;
- qualquer divergência encontrada.

Se houver qualquer divergência, pare e reporte:

```text
NO_GO_INTEGRITY_FAILURE
```
