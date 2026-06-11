# Mensagem para Devin — Início da Implementação do AI Agent Architecture OS

Estou iniciando a implementação do **AI Agent Architecture OS** neste repositório.

O conteúdo do pacote `plano_implementacao_devin_ai_agent_os_v2_1.zip` já foi reconstruído, validado, extraído e deve estar commitado no repositório em:

```text
plano_implementacao_devin_ai_agent_os_v2/
```

Trate essa árvore documental como a **fonte oficial principal** para conduzir esta sessão.

## Objetivo imediato

Antes de qualquer alteração no repositório, faça somente o **bootstrap da sessão mãe-orquestradora**, em modo de investigação, leitura e planejamento.

Nesta etapa inicial, não implemente código, não mova arquivos, não remova instruções, não arquive documentos, não execute sanitização real e não realize ações destrutivas.

## Ordem obrigatória inicial de leitura

Localize e leia, nesta ordem:

1. `plano_implementacao_devin_ai_agent_os_v2/75_DEVIN_ORCHESTRATION/MASTER_DEVIN_ORCHESTRATION_GUIDE.md`
2. `plano_implementacao_devin_ai_agent_os_v2/75_DEVIN_ORCHESTRATION/DEVIN_IMPLEMENTATION_PLAN.md`
3. `plano_implementacao_devin_ai_agent_os_v2/00_CONTROLE/HANDOFF_FINAL_PARA_DEVIN_IMPLEMENTACAO.md`
4. `plano_implementacao_devin_ai_agent_os_v2/00_CONTROLE/MATRIZ_GO_NO_GO_FINAL_PRE_DEVIN.md`
5. `plano_implementacao_devin_ai_agent_os_v2/MATRIZES/MATRIZ_FASE_GATE_STATUS_TRANSICAO.md`
6. `plano_implementacao_devin_ai_agent_os_v2/75_DEVIN_ORCHESTRATION/STATUS_TAXONOMY_AND_TRANSITION_POLICY.md`
7. `plano_implementacao_devin_ai_agent_os_v2/75_DEVIN_ORCHESTRATION/REPOSITORY_SNAPSHOT_INTAKE_AND_SANITIZATION_READINESS_GATE.md`
8. `plano_implementacao_devin_ai_agent_os_v2/75_DEVIN_ORCHESTRATION/EXTERNAL_POLICY_REFERENCE_CATALOG.md`
9. `plano_implementacao_devin_ai_agent_os_v2/75_DEVIN_ORCHESTRATION/DEEPWIKI_CONTEXT_RETRIEVAL_POLICY.md`
10. `plano_implementacao_devin_ai_agent_os_v2/00_AUDITORIA_FINAL_EXAUSTIVA/MAPA_AUTORIDADE_PRELIMINAR.md`

Se algum desses arquivos não existir, pare a execução operacional, reporte exatamente quais arquivos estão ausentes e classifique o estado como:

```text
BLOCKED_BY_MISSING_INPUT
```

## Confirmações obrigatórias após a leitura

Depois da leitura inicial, confirme explicitamente que entendeu:

1. a hierarquia de autoridade documental;
2. qual handoff é atual e quais artefatos são históricos;
3. a diferença entre `Execution Status`, `Criterion Assessment`, `Readiness Decision` e `Operational State`;
4. que a decisão atual é:

```text
GO_WITH_WARNINGS_FOR_DEVIN_IMPLEMENTATION
```

5. que a ausência ou necessidade de snapshot deve ser tratada pelo `Snapshot Intake Gate`;
6. que sanitização real, arquivamento, remoção, migração, renomeação ou qualquer ação destrutiva dependem de snapshot válido e aprovação humana;
7. que DeepWiki, se usado, deve funcionar como índice/localizador, não como fonte final de verdade;
8. que referências externas ausentes devem ser tratadas conforme o `EXTERNAL_POLICY_REFERENCE_CATALOG.md`;
9. que nenhuma implementação deve começar antes de passar pelos gates adequados;
10. que toda decisão relevante deve ser registrada com evidência, status e risco residual.

## Relatório de bootstrap esperado

Após a leitura, produza um relatório curto e objetivo contendo:

1. **Arquivos encontrados**
   - Liste os arquivos obrigatórios encontrados.
   - Liste arquivos ausentes, se houver.

2. **Mapa de autoridade confirmado**
   - Indique quais documentos são normativos atuais.
   - Indique quais documentos são históricos ou superseded.

3. **Interpretação da fase atual**
   - Diga em qual fase do plano estamos.
   - Explique se a sessão deve operar em Ask Mode, Agent Mode ou modo híbrido, conforme os gates.

4. **Estado operacional**
   - Informe o `Operational State` inicial.
   - Se ainda não houver snapshot válido, registre:

```text
REPOSITORY_SNAPSHOT_REQUIRED
```

5. **Riscos imediatos**
   - Liste riscos de contexto insuficiente.
   - Liste riscos de contexto excessivo.
   - Liste riscos de ações prematuras.

6. **Perguntas ao usuário**
   - Faça somente perguntas realmente necessárias para avançar.
   - Separe perguntas bloqueantes de perguntas não bloqueantes.

7. **Plano da Fase 1 — Preparação e Sanitização**
   - Proponha o plano de execução da Fase 1.
   - Separe o que pode ser feito sem snapshot do que exige snapshot.
   - Aponte gates de entrada e saída.
   - Aponte evidências mínimas necessárias.

## Restrições obrigatórias

Não altere arquivos ainda.

Não implemente código ainda.

Não mova, remova, renomeie, arquive, deprecie ou migre instruções ainda.

Não execute sanitização real ainda.

Não use documentação histórica como normativa atual.

Não use DeepWiki como evidência final.

Não trate outputs iguais como prova suficiente de equivalência.

Não avance para implementação sem passar pelos gates definidos.

Não execute ações destrutivas sem snapshot válido, justificativa, plano de rollback e aprovação humana.

## Critério de parada

Ao concluir o bootstrap, pare e aguarde minha aprovação explícita para avançar.

O resultado esperado desta primeira etapa é:

```text
PASS_BOOTSTRAP_READY_FOR_HUMAN_REVIEW
```

ou, se houver problema de insumo:

```text
BLOCKED_BY_MISSING_INPUT
```

ou, se houver conflito documental real:

```text
BLOCKED_BY_CONFLICT
```
