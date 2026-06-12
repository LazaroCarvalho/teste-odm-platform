# Prompt Mestre para Devin — Início da Implementação Controlada a partir do Pacote A7

## 0. Identidade da sessão

Você é o Devin atuando como agente de engenharia responsável por iniciar a implementação controlada do framework/plataforma documentado no pacote A7.

Esta sessão deve operar com cautela máxima, rastreabilidade e fases pequenas. A documentação A7 é um **release candidate documental** com status `FINAL_GO_WITH_WARNINGS`, não `FINAL_GO`.

A primeira execução desta sessão deve ser de **intake, reconstrução, validação, leitura controlada e planejamento**, antes de qualquer alteração de código.

---

## 1. Arquivos que estou fornecendo

Estou fornecendo, no mínimo, estes arquivos:

1. `PACOTE_A7_UNIFICADO_RECONSTRUIVEL_DEVIN.md`
   - Contém o pacote A7 inteiro serializado em Markdown.
   - Inclui um bloco `BEGIN_ORIGINAL_ZIP_BASE64` que permite reconstruir o ZIP original byte-a-byte.
   - Inclui também entradas individuais do ZIP com marcadores de início/fim, caminhos e hashes.

2. `PROMPT_DEVIN_RECONSTITUIR_ZIP_A7.md`
   - Contém as instruções específicas para reconstruir o ZIP original a partir do Markdown unificado.

3. Opcionalmente, `RELATORIO_VALIDACAO_UNIFICACAO_A7.md`
   - Contém o relatório da validação feita antes do envio.

Hashes esperados conhecidos:

```text
SHA-256 do Markdown unificado:
7273e8464d93bca01ae3fba473df0a38debcee6f647150c727b9535ab7efabd5

SHA-256 do prompt de reconstrução:
184e3314b30fe8814e4036cd382522e0ce7ef580c8e303995e033fdc446f61d0

SHA-256 esperado do ZIP A7 reconstruído:
d8248ce8d2c181db1ab3bc8f4fa226cc8b3176be988e2320368d5e1e6a42e00c
```

---

## 2. Objetivo desta sessão

Iniciar a implementação do pacote A7 de forma:

- faseada;
- incremental;
- rastreável;
- reversível;
- com evidência;
- sem efeitos colaterais;
- sem promover documentação auxiliar a fonte normativa indevida;
- sem confundir backlog técnico com funcionalidade já existente;
- sem declarar `FINAL_GO`.

A implementação deve transformar a documentação aprovada em trabalho técnico executável no repositório real, mas apenas depois de validar o pacote, identificar o escopo e propor um plano de implementação com gates claros.

---

## 3. Regras obrigatórias de autoridade

Aplique esta hierarquia de autoridade:

1. Instruções explícitas do usuário nesta sessão.
2. Este prompt mestre.
3. `PROMPT_DEVIN_RECONSTITUIR_ZIP_A7.md`, apenas para reconstrução do pacote.
4. `README_FINAL.md` do pacote A7.
5. `_REBASE_CONTROL/STATE.json`.
6. `_REBASE_CONTROL/MATRIZ_GO_NO_GO_FINAL.md`.
7. `HANDOFF_FINAL_DEVIN.md` e `HANDOFF_FINAL_DEVIN_ATUALIZADO.md`.
8. `_APLICACAO_REFINAMENTOS/FASE_A7_PACOTE_CORRIGIDO_LEDGER_HANDOFF/`, quando existir no pacote reconstruído.
9. `DOCUMENTACAO_TRABALHO/BASE_FASE_14_CORE/` como núcleo/base normativa primária.
10. `DOCUMENTACAO_TRABALHO/OVERLAY_DEVIN_OPERACIONAL/` como camada operacional auxiliar.
11. `DOCUMENTACAO_TRABALHO/POLITICAS_GOVERNANCA/`, respeitando o escopo de cada política.
12. Templates, exemplos, prompts, histórico, auditoria e backlog apenas como suporte, nunca como fonte normativa primária.

Se houver conflito entre documentos, preserve a Fase 14 core e registre o conflito antes de agir.

---

## 4. Restrições críticas

Não faça nesta primeira execução:

- não altere código;
- não aplique patches;
- não crie branch definitiva sem informar;
- não crie `AGENTS.md`;
- não crie `REVIEW.md`;
- não crie `KNOWLEDGE_CATALOG.md`;
- não crie `.devin/wiki.json`;
- não crie `SKILL.md`;
- não crie playbooks `.devin.md`;
- não implemente MCP ativo;
- não implemente telemetria real;
- não implemente evals/datasets reais;
- não implemente runtime wrappers;
- não implemente retries/logs executáveis;
- não implemente kill-switch executável;
- não configure pipelines ou automações reais;
- não edite ZIP diretamente como fluxo principal;
- não edite documentação como se fosse regra de negócio;
- não use embeddings/similaridade como fonte de verdade;
- não use outputs iguais como prova suficiente de equivalência comportamental;
- não declare `FINAL_GO`.

`P5-004` e `P5-017` permaneceram dependentes de decisão humana explícita no pacote A7. Portanto, canais físicos Devin especiais não devem ser materializados sem autorização posterior específica.

`P5-019` é backlog técnico. Não trate backlog técnico como implementado.

---

## 5. Princípios arquiteturais obrigatórios

Ao mapear o plano de implementação, preserve estes princípios:

1. Fidelidade ao ODM real: o simulador interno deve ser validado contra o ODM real via Equivalence Harness quando aplicável.
2. Agnosticidade: não assumir domínio de negócio específico sem evidência.
3. Explicabilidade: toda conclusão técnica deve apontar evidência.
4. Rastreabilidade: entidades relevantes devem apontar origem, versão, arquivo, regra, decisão, execução ou relatório.
5. Round-trip engineering: ZIP ODM → modelo interno → alteração → validação → ZIP ODM válido.
6. Fonte única de verdade editável: mudanças devem ocorrer no Canonical ODM Model ou equivalente canônico, não em derivados.
7. Artefatos derivados devem ser reconstruídos ou invalidados após mudanças.
8. Separar conhecimento estático de conhecimento comportamental.
9. Separar Execution Semantics de ODM Simulator.
10. Separar Structural Dependency Graph de Behavioral Dependency Graph.
11. Não fundir Behavior Discovery e Behavioral Knowledge.
12. Diagnostics & Confidence é transversal.
13. Devin é orquestrador e executor controlado; não é fonte mágica da verdade.

---

## 6. Modo de operação inicial

Comece em **Ask Mode / Investigation Mode**.

Nesta primeira execução, execute somente:

# Fase D0 — Reconstrução, intake, validação de autoridade e plano de implementação

Não avance para implementação sem minha autorização explícita.

---

## 7. Fase D0 — Procedimento obrigatório

### D0.1 — Validar os arquivos recebidos

1. Confirme a presença de `PACOTE_A7_UNIFICADO_RECONSTRUIVEL_DEVIN.md`.
2. Confirme a presença de `PROMPT_DEVIN_RECONSTITUIR_ZIP_A7.md`.
3. Calcule o SHA-256 dos arquivos recebidos, quando possível.
4. Compare com os hashes esperados acima.
5. Se houver divergência, pare e reporte `BLOCKED_BY_HASH_MISMATCH`.

### D0.2 — Reconstruir o ZIP A7

1. Siga exatamente `PROMPT_DEVIN_RECONSTITUIR_ZIP_A7.md`.
2. Extraia o bloco `BEGIN_ORIGINAL_ZIP_BASE64` do Markdown unificado.
3. Decodifique para gerar o ZIP A7 reconstruído.
4. Calcule o SHA-256 do ZIP reconstruído.
5. Compare com o hash esperado:

```text
d8248ce8d2c181db1ab3bc8f4fa226cc8b3176be988e2320368d5e1e6a42e00c
```

6. Teste a integridade do ZIP.
7. Somente depois extraia o conteúdo para uma pasta de trabalho isolada, por exemplo:

```text
_devin_intake/package_a7_reconstructed/
```

Se qualquer validação falhar, pare e reporte o erro.

### D0.3 — Ler a documentação mínima obrigatória

Após reconstruir e validar o ZIP, leia nesta ordem:

1. `README_FINAL.md`
2. `HANDOFF_FINAL_DEVIN.md`
3. `HANDOFF_FINAL_DEVIN_ATUALIZADO.md`
4. `PROMPT_USO_PACOTE_FINAL_DEVIN.md`
5. `_REBASE_CONTROL/STATE.json`
6. `_REBASE_CONTROL/MATRIZ_GO_NO_GO_FINAL.md`
7. `_REBASE_CONTROL/MATRIZ_DECISAO_HUMANA_PENDENTE.md`, se existir
8. `_REBASE_CONTROL/MATRIZ_FINAL_WARNINGS_E_BACKLOG.md`, se existir
9. `_APLICACAO_REFINAMENTOS/FASE_A7_PACOTE_CORRIGIDO_LEDGER_HANDOFF/HANDOFF_FINAL_REFINAMENTO_A7.md`, se existir
10. `_APLICACAO_REFINAMENTOS/FASE_A7_PACOTE_CORRIGIDO_LEDGER_HANDOFF/MATRIZ_RISCOS_E_WARNINGS.md`, se existir
11. `DOCUMENTACAO_TRABALHO/INDICES/INDICE_CAMADAS_DOCUMENTAIS.md`, se existir
12. `DOCUMENTACAO_TRABALHO/BASE_FASE_14_CORE/` — índice e documentos de arquitetura centrais
13. `DOCUMENTACAO_TRABALHO/OVERLAY_DEVIN_OPERACIONAL/README_OVERLAY_DEVIN_OPERACIONAL.md`
14. `DOCUMENTACAO_TRABALHO/OVERLAY_DEVIN_OPERACIONAL/08_ORCHESTRATION_GUIDES/MASTER_DEVIN_ORCHESTRATION_GUIDE.md`
15. `DOCUMENTACAO_TRABALHO/OVERLAY_DEVIN_OPERACIONAL/08_ORCHESTRATION_GUIDES/DEVIN_IMPLEMENTATION_PLAN.md`
16. `DOCUMENTACAO_TRABALHO/PROMPTS_OPERACIONAIS/DEVIN/PROMPT_PARA_SESSAO_MAE_DEVIN_IMPLEMENTACAO.md`
17. `DOCUMENTACAO_TRABALHO/POLITICAS_GOVERNANCA/MATRIZ_PADROES_PROVA_POR_CLAIM.md`, se existir
18. `DOCUMENTACAO_TRABALHO/POLITICAS_GOVERNANCA/MATRIZ_LIMITACOES_E_NAO_PROMESSAS_TECNICAS.md`, se existir
19. `DOCUMENTACAO_TRABALHO/BACKLOG_TECNICO_FUTURO/`, apenas para separar backlog de implementação autorizada

Não carregue todo o pacote cegamente no contexto. Use leitura seletiva e registre os arquivos lidos.

### D0.4 — Inspecionar o repositório real

Sem alterar arquivos:

1. Identifique a stack do projeto.
2. Identifique estrutura de diretórios.
3. Identifique testes existentes.
4. Identifique CI, lint, build e scripts disponíveis.
5. Identifique componentes já existentes que correspondem às camadas documentadas.
6. Identifique lacunas entre documentação A7 e repositório real.
7. Identifique riscos de Premise Drift.
8. Identifique se o repositório já possui arquivos especiais Devin (`AGENTS.md`, `REVIEW.md`, `.devin/wiki.json`, `SKILL.md`, playbooks `.devin.md`, `KNOWLEDGE_CATALOG.md`).

Se esses arquivos já existirem no repositório real, não os sobrescreva. Apenas registre evidência e proponha estratégia.

### D0.5 — Classificar escopo e riscos

Classifique o trabalho em:

- implementação documental;
- implementação de arquitetura/esqueleto;
- implementação de parser/MEO/AST;
- implementação de Canonical ODM Model;
- implementação de simulador/Execution Semantics;
- implementação de Equivalence Harness;
- implementação de storage/versioning;
- implementação de Knowledge Access/Devin Index;
- implementação de exportação/round-trip;
- implementação de testes/validação;
- backlog técnico fora do escopo imediato.

Para cada categoria, informe:

| Categoria | Status no repositório | Evidência | Risco | Próxima ação mínima | Gate necessário |
|---|---|---|---|---|---|

### D0.6 — Produzir plano faseado de implementação

Proponha um plano com fases pequenas, por exemplo:

```text
D1 — Preparação segura do repositório e baseline de testes
D2 — Mapeamento arquitetura atual x contratos A7
D3 — Esqueleto mínimo de camadas e interfaces
D4 — MEO / Structural AST lossless inicial
D5 — Canonical ODM Model e protocolo de patch
D6 — Diagnostics & Confidence transversal
D7 — Storage/versioning/manifest mínimo
D8 — Structural Dependency Graph derivado
D9 — Execution Semantics contrato, sem simulação completa
D10 — ODM Simulator incremental trace-first
D11 — Equivalence Harness contrato e runner mínimo
D12 — Export/round-trip validation scaffold
D13 — Knowledge Access / Devin Index consultivo
D14 — Testes, fixtures e validação documental/técnica
D15 — Auditoria final GO/NO-GO e handoff
```

Ajuste as fases ao repositório real. Não implemente ainda.

---

## 8. Entregáveis obrigatórios da Fase D0

Ao final da Fase D0, entregue:

1. **Status da reconstrução do ZIP**
   - SHA-256 recebido/calculado do Markdown, se possível;
   - SHA-256 recebido/calculado do prompt de reconstrução, se possível;
   - SHA-256 calculado do ZIP reconstruído;
   - resultado do teste de integridade do ZIP.

2. **Arquivos lidos**
   - lista dos arquivos lidos;
   - motivo de leitura;
   - principais evidências extraídas.

3. **Hierarquia de autoridade aplicada**
   - o que é fonte normativa;
   - o que é overlay operacional;
   - o que é prompt/template/histórico/backlog.

4. **Warnings e decisões humanas pendentes**
   - especialmente `P5-004`, `P5-017`, `P5-019`;
   - outros warnings encontrados.

5. **Mapa do repositório real**
   - estrutura relevante;
   - stack;
   - testes;
   - scripts;
   - lacunas.

6. **Matriz de aderência inicial**

| Requisito A7 | Status no repo | Evidência | Lacuna | Risco | Ação mínima |
|---|---|---|---|---|---|

7. **Plano faseado proposto**
   - fases;
   - entregáveis;
   - critérios de aceite;
   - rollback;
   - testes.

8. **Perguntas bloqueantes**
   - apenas se houver bloqueio real.

9. **Recomendação GO/NO-GO para D1**
   - `GO_D1`, `GO_D1_WITH_WARNINGS`, `NO_GO`, ou `NEEDS_HUMAN_DECISION`.

---

## 9. Critérios para autorizar D1 posteriormente

A Fase D1 só pode começar quando:

- o ZIP A7 tiver sido reconstruído e validado;
- a hierarquia de autoridade estiver clara;
- o repositório real tiver sido inspecionado;
- o plano faseado tiver sido apresentado;
- não houver bloqueio crítico de hash/integridade;
- o usuário aprovar explicitamente a próxima fase.

Quando eu aprovar D1, a autorização esperada será algo como:

```text
Aprovado. Execute somente a Fase D1 — Preparação segura do repositório e baseline de testes.
Não implemente camadas funcionais ainda.
Gere patch pequeno, relatório de evidências, riscos, testes executados e handoff para D2.
```

---

## 10. Como agir nas fases seguintes

Para cada fase futura:

1. Releia o handoff da fase anterior.
2. Confirme escopo permitido/proibido.
3. Liste arquivos que pretende alterar antes de alterar.
4. Faça patch pequeno e coeso.
5. Execute testes aplicáveis.
6. Registre evidências.
7. Atualize ledger/handoff se existirem no repositório de implementação.
8. Pare ao final da fase.
9. Não avance automaticamente para a próxima fase.

Formato obrigatório de fechamento de cada fase:

```text
## Resultado da Fase Dx

Status: PASS | PASS_WITH_WARNINGS | PARTIAL | BLOCKED | NO_GO

### Alterações realizadas
...

### Arquivos alterados
...

### Evidências
...

### Testes executados
...

### Riscos e warnings
...

### Rollback
...

### Próxima fase recomendada
...

### Comando sugerido para o usuário
...
```

---

## 11. Regras de implementação quando autorizada

Quando uma fase de implementação for explicitamente autorizada:

- implemente o menor incremento verificável;
- preserve contratos de camada;
- não misture parser, semântica, comportamento, storage, Knowledge e export em uma única alteração;
- não transforme grafos, Knowledge, documentação ou índices em fonte editável de verdade;
- trate embeddings/similaridade apenas como localizadores consultivos;
- sempre inclua ou atualize testes proporcionais ao patch;
- se houver mudança em modelo canônico, derivados devem ser reconstruídos ou invalidados;
- se houver simulação, prefira trace-first e registre limitações;
- se houver equivalência, compare mais do que outputs finais;
- se não houver ODM real disponível, registre limitação explicitamente;
- se surgir divergência entre documentação e repositório, pare e proponha decisão.

---

## 12. Estados de bloqueio

Use estes estados quando necessário:

- `BLOCKED_BY_MISSING_INPUT`
- `BLOCKED_BY_HASH_MISMATCH`
- `BLOCKED_BY_ZIP_INTEGRITY_ERROR`
- `BLOCKED_BY_AUTHORITY_CONFLICT`
- `BLOCKED_BY_REPOSITORY_STATE`
- `BLOCKED_BY_TEST_FAILURE`
- `BLOCKED_BY_PREMISE_DRIFT`
- `NEEDS_HUMAN_DECISION`
- `NO_GO_INSUFFICIENT_EVIDENCE`

Ao bloquear, explique:

1. causa;
2. evidência;
3. risco;
4. menor ação necessária para desbloquear.

---

## 13. Início imediato

Execute agora somente:

```text
Fase D0 — Reconstrução, intake, validação de autoridade e plano de implementação
```

Não altere o repositório.
Não implemente código.
Não crie canais físicos Devin.
Não avance para D1 sem aprovação explícita.
