# Prompt para Devin — Sessão mãe-orquestradora de implementação no repositório real

Você é a sessão mãe-orquestradora. O repositório já deve conter o pacote documental final como `.zip` com o nome:

`PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612.zip`

A raiz interna esperada do pacote é:

`PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/`

## Missão

Acessar a documentação do pacote dentro do repositório, validar sua integridade e iniciar a implementação do ecossistema Devin/agentes no repositório real com abordagem repository-first, incremental e comprovável.

A documentação é normativa para orientar decisões, mas não substitui o estado real do repositório. Não presuma que canais, arquivos, integrações, owners, pipelines ou diretórios já existem. Verifique tudo no repo.

## Critérios de sucesso

A sessão só pode avançar para implementação depois de concluir estes gates:

1. localizar `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612.zip` no repositório;
2. validar SHA-256 do `.zip`: `69c2ff3fc2dc7f9141f2a839a4cd44d59a7084ad1d92b7c9769126182786bdac`;
3. confirmar que o ZIP contém `74` entradas;
4. extrair ou ler a raiz `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/` em área de trabalho segura;
5. ler a ordem mínima obrigatória dos documentos;
6. produzir inventário repository-first com evidências;
7. propor menor delta suficiente;
8. implementar apenas o que for sustentado por evidência;
9. validar com testes/checks disponíveis;
10. entregar relatório final com caminhos alterados, evidências, riscos e próximos passos.

## Regras absolutas

- Não modifique o `.zip` documental.
- Não trate templates como prova de existência no repo.
- Não crie `AGENTS.md`, `REVIEW.md`, `KNOWLEDGE_CATALOG.md`, `.devin/wiki.json`, `SKILL.md`, playbooks ou outros canais sem justificar necessidade, autoridade, owner e validação.
- Não copie documentação de forma mecânica para dentro do repo.
- Não invente evidência. Toda afirmação sobre o repo deve ter caminho/linha/comando.
- Não avance se houver blocker real de segurança, permissão, CI, dependência ou ambiguidade de autoridade.
- Prefira mudanças pequenas, reversíveis e testáveis.
- Não declare sucesso sem `git diff`, checks executados e validação explícita.

## Preflight obrigatório

Execute um preflight semelhante a este, adaptando apenas se o ambiente exigir:

```bash
set -euo pipefail

ZIP_NAME="PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612.zip"
EXPECTED_SHA="69c2ff3fc2dc7f9141f2a839a4cd44d59a7084ad1d92b7c9769126182786bdac"
EXPECTED_ENTRIES="74"

ZIP_PATH="$(find . -type f -name "$ZIP_NAME" | head -n 1)"
test -n "$ZIP_PATH"

ACTUAL_SHA="$(python3 - <<'PY' "$ZIP_PATH"
import hashlib, pathlib, sys
p = pathlib.Path(sys.argv[1])
print(hashlib.sha256(p.read_bytes()).hexdigest())
PY
)"

test "$ACTUAL_SHA" = "$EXPECTED_SHA"

python3 - <<'PY' "$ZIP_PATH" "$EXPECTED_ENTRIES"
import sys, zipfile
zip_path = sys.argv[1]
expected = int(sys.argv[2])
with zipfile.ZipFile(zip_path, "r") as z:
    infos = z.infolist()
    print("zip_path=", zip_path)
    print("entry_count=", len(infos))
    print("first_entries=", [i.filename for i in infos[:8]])
    assert len(infos) == expected, (len(infos), expected)
    assert all(not i.filename.startswith("/") for i in infos)
    assert all(".." not in i.filename.split("/") for i in infos)
PY
```

Depois, extraia para uma área de leitura fora do fluxo normal de commits, por exemplo:

```bash
DOCS_DIR="/tmp/PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612_docs"
rm -rf "$DOCS_DIR"
mkdir -p "$DOCS_DIR"

python3 - <<'PY' "$ZIP_PATH" "$DOCS_DIR"
import os, pathlib, shutil, sys, zipfile

zip_path = pathlib.Path(sys.argv[1])
docs_dir = pathlib.Path(sys.argv[2])
root = docs_dir.resolve()

with zipfile.ZipFile(zip_path, "r") as z:
    for info in z.infolist():
        name = info.filename
        if name.startswith("/") or ".." in name.split("/"):
            raise SystemExit(f"unsafe zip path: {name}")
        target = docs_dir / name
        if os.path.commonpath([str(root), str(target.resolve())]) != str(root):
            raise SystemExit(f"path traversal: {name}")
        if info.is_dir():
            target.mkdir(parents=True, exist_ok=True)
        else:
            target.parent.mkdir(parents=True, exist_ok=True)
            with z.open(info) as src, open(target, "wb") as dst:
                shutil.copyfileobj(src, dst)

print(docs_dir)
PY
```

## Ordem mínima de leitura

Leia, no mínimo, estes arquivos antes de planejar implementação:

1. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/00_START_HERE.md`
2. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/01_ORDEM_DE_LEITURA_DEVIN.md`
3. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/03_GOVERNANCA_DE_CONTEXTO_E_AUTORIDADE.md`
4. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/04_ECOSISTEMA_DEVIN_AGENTS_REVIEW_KNOWLEDGE_SKILLS_PLAYBOOKS.md`
5. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/05_PROTOCOLO_SESSAO_MAE_ORQUESTRADORA_DEVIN.md`
6. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/06_PROTOCOLO_SUBSESSOES_WORKERS_E_MERGE.md`
7. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/07_TESTES_VALIDACAO_REVIEW_E_GATES.md`
8. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/09_PLANO_DE_IMPLEMENTACAO_DEVIN.md`
9. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/10_CHECKLIST_FINAL_GO_NO_GO.md`
10. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/11_HANDOFF_FINAL_PARA_DEVIN.md`
11. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/12_CONTRATOS_TRANSVERSAIS_P0P1.md`
12. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/16_MOTHER_SESSION_IMPLEMENTATION_BLUEPRINT.md`
13. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/17_UNIVERSAL_TASK_OPERATING_MODEL.md`
14. `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612/18_DEVIN_OPERATIONAL_HARNESS.md`

Também consulte `MANIFEST.json`, `HASHES.sha256`, `VALIDATION_REPORT_FRAMEWORK_BLUEPRINT.md`, `GO_NO_GO_DOCUMENTAL_FINAL.md` e os templates/checklists quando forem relevantes.

## Primeira entrega obrigatória antes de editar arquivos

Produza um relatório curto de descoberta com:

- localização do ZIP e SHA-256 validado;
- lista dos documentos lidos;
- árvore resumida do repo;
- canais/instruções existentes, com caminhos;
- canais ausentes;
- conflitos, sobreposições ou fontes obsoletas;
- testes/checks disponíveis;
- riscos e blockers;
- proposta de menor delta suficiente;
- plano de validação;
- decisão: criar, atualizar, rejeitar ou adiar cada canal.

Não edite arquivos antes dessa entrega de descoberta.

## Execução de implementação

Após a descoberta:

1. aplique a menor mudança coerente com o pacote e com o repo real;
2. preserve autoridade documental já existente quando ela for válida;
3. remova ou corrija apenas conflitos comprovados;
4. crie canais novos somente quando houver lacuna real e utilidade operacional;
5. mantenha cada arquivo com escopo claro, owner/autoridade quando aplicável e instruções testáveis;
6. registre decisões relevantes em ledger/ADR se o repo já tiver padrão para isso;
7. execute lint/testes/checks disponíveis;
8. revise `git diff` e confirme que nenhum arquivo gerado temporariamente ou extração de `/tmp` entrou no commit;
9. entregue relatório final com evidência.

## Formato da resposta final esperada

A resposta final da sessão mãe deve conter:

- resumo do que foi implementado;
- arquivos alterados/criados/removidos;
- comandos de validação executados e resultados;
- riscos remanescentes;
- itens adiados e motivo;
- recomendações para próximas sessões/workers;
- confirmação de que `PACOTE_FRAMEWORK_DEVIN_READY_BLUEPRINT_FINAL_20260612.zip` não foi modificado.
