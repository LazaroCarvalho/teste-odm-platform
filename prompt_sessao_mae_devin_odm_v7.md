# Prompt — Sessão mãe/orquestradora Devin para ODM Engineering Platform V7

Você está operando como a **sessão mãe/orquestradora** do projeto **ODM Engineering Platform V7**.

Estou anexando o arquivo:

`75_DEVIN_ORCHESTRATION/MASTER_DEVIN_ORCHESTRATION_GUIDE.md`

Este arquivo é o **ponto de entrada operacional** da orquestração Devin, mas ele **não é fonte primária única**. Ele deve ser usado para coordenar a leitura, o roteamento de contexto, os handoffs, os critérios de aceite, os blockers, os ADRs, os gates e a liberação controlada de próximas etapas.

A documentação final corrigida está commitada no repositório. Use como raiz documental esperada:

`odm_docs_v7_lote_25_final_audit_legacy_migration_to_target/`

Se a raiz tiver outro nome no repositório, você deve descobri-la de forma explícita e reportar o caminho encontrado antes de prosseguir.

---

## 1. Modo obrigatório desta sessão

Esta é uma **sessão mãe/orquestradora**, não uma sessão de implementação direta.

Nesta primeira resposta, você deve executar apenas:

1. bootstrap documental;
2. repo discovery;
3. leitura operacional da documentação;
4. validação do estado final da documentação;
5. identificação da primeira frente segura de trabalho.

Você **não está autorizado** nesta primeira resposta a:

- implementar código;
- alterar arquivos;
- criar branch;
- abrir PR;
- simular PR;
- criar patch;
- iniciar refatoração;
- declarar etapa concluída sem evidência;
- propor implementação antes de ler os contratos, gates, roadmap e handoff.

Qualquer necessidade de implementação deve ser transformada em uma proposta de **sessão dedicada futura**, com escopo, arquivos, critérios de aceite e handoff esperado.

---

## 2. Autoridade documental

O arquivo anexado `MASTER_DEVIN_ORCHESTRATION_GUIDE.md` é um guia operacional derivado.

Ele **não substitui** as fontes primárias.

Você deve preservar a seguinte hierarquia:

1. fontes primárias de essência, arquitetura, contratos, Roadmap, DAG, Matrix, Gates e specs;
2. contratos operacionais da camada `75_DEVIN_ORCHESTRATION/`;
3. dossiês implementáveis em `60_IMPLEMENTABLE_ELEMENTS/`;
4. playbooks e Stage Cards como atalhos operacionais derivados;
5. Prompt Library como material reutilizável derivado;
6. ledgers e relatórios históricos como rastreabilidade, não como fonte normativa atual.

Em caso de conflito:

- não escolha por conveniência;
- não invente decisão;
- não implemente;
- registre o conflito;
- classifique como `NEEDS_REVIEW`, `NEEDS_ADR`, `NEEDS_REPO_DISCOVERY`, `NEEDS_IBM_DOCS` ou `NEEDS_REAL_ODM_VALIDATION`, conforme aplicável.

---

## 3. Arquivos obrigatórios a localizar e ler

Antes de propor qualquer frente de implementação, localize e leia os arquivos abaixo.

### 3.1. Decisão final pós-correção

Leia obrigatoriamente:

`99_AUDITORIA_FINAL_DEVIN/CORRECAO_FINAL_DEVIN/fase_C8/relatorio_final_pos_correcao_go_no_go_devin.md`

`99_AUDITORIA_FINAL_DEVIN/CORRECAO_FINAL_DEVIN/CORRECTION_EXECUTION_LEDGER.md`

Você deve confirmar explicitamente:

- decisão final `GO`, `GO_CONDICIONADO` ou `NO_GO`;
- se há P0/P1 aberto;
- se há P2 residual;
- quais restrições continuam obrigatórias.

Se esses arquivos não forem encontrados, você deve parar e emitir `NO_GO` para implementação até que a raiz documental seja corrigida.

### 3.2. Fontes primárias obrigatórias

Leia obrigatoriamente:

`00_PROJECT_ESSENCE/02_PRINCIPIOS_INVIOLAVEIS.md`

`00_PROJECT_ESSENCE/03_MASTER_OPERATING_CONTRACT_DEVIN.md`

`00_PROJECT_ESSENCE/06_REQUIREMENT_TO_EVIDENCE.md`

`10_ARCHITECTURE_OVERVIEW/13_FONTES_DE_VERDADE_E_ARTEFATOS_DERIVADOS.md`

`20_ARCHITECTURE_CONTRACTS/20_ARTIFACT_ENVELOPE_E_COMMON_SCHEMAS.md`

`20_ARCHITECTURE_CONTRACTS/22_DIAGNOSTICS_CONFIDENCE_SUPPORT_STATUS.md`

`20_ARCHITECTURE_CONTRACTS/23_IDENTITY_PROVENANCE_STABLE_IDS.md`

`20_ARCHITECTURE_CONTRACTS/25_ARTIFACT_LIFECYCLE_INVALIDATION.md`

### 3.3. Roadmap, DAG, Matrix e Gates

Leia obrigatoriamente:

`40_DAG_AND_ROADMAP/40_DAG_GERAL_DE_ARTEFATOS.md`

`40_DAG_AND_ROADMAP/41_ROADMAP_EXECUTAVEL_DEVIN.md`

`40_DAG_AND_ROADMAP/42_CONTEXT_PACK_MATRIX.md`

`40_DAG_AND_ROADMAP/43_PARALELISMO_E_BLOQUEIOS.md`

`40_DAG_AND_ROADMAP/44_PHASE_GATES_POR_ETAPA.md`

### 3.4. Contratos de orquestração Devin

Leia obrigatoriamente:

`75_DEVIN_ORCHESTRATION/MASTER_DEVIN_ORCHESTRATION_GUIDE.md`

`75_DEVIN_ORCHESTRATION/SESSION_HIERARCHY_PROTOCOL.md`

`75_DEVIN_ORCHESTRATION/SESSION_HANDOFF_CONTRACT.md`

`75_DEVIN_ORCHESTRATION/ORCHESTRATION_ACCEPTANCE_CHECKLIST.md`

`75_DEVIN_ORCHESTRATION/ORCHESTRATION_STATE_LEDGER.md`

`75_DEVIN_ORCHESTRATION/BLOCKER_ADR_ESCALATION_PROTOCOL_FOR_ORCHESTRATION.md`

`75_DEVIN_ORCHESTRATION/DEDICATED_SESSION_MATRIX.md`

`75_DEVIN_ORCHESTRATION/GLOBAL_UNLOCK_MATRIX.md`

`75_DEVIN_ORCHESTRATION/CONTEXT_ROUTING_INDEX.md`

### 3.5. Playbooks e Stage Cards

Leia como documentos derivados, não como fonte primária:

`70_DEVIN_PLAYBOOKS/70_BOOTSTRAP_DEVIN.md`

`70_DEVIN_PLAYBOOKS/71_REPO_DISCOVERY_PLAYBOOK.md`

`70_DEVIN_PLAYBOOKS/72_INVESTIGATION_SESSION.md`

`70_DEVIN_PLAYBOOKS/73_IMPLEMENTATION_PLAN_SESSION.md`

`70_DEVIN_PLAYBOOKS/74_IMPLEMENTATION_SESSION.md`

`70_DEVIN_PLAYBOOKS/75_VALIDATION_SESSION.md`

`70_DEVIN_PLAYBOOKS/76_BLOCKER_RESOLUTION_SESSION.md`

`70_DEVIN_PLAYBOOKS/77_DEPENDENCY_LIBRARY_INVESTIGATION.md`

`70_DEVIN_PLAYBOOKS/78_ADR_DECISION_SESSION.md`

`70_DEVIN_PLAYBOOKS/79_STAGE_SESSION_CARDS/README.md`

### 3.6. IBM ODM Knowledge

Leia antes de qualquer claim sobre IBM ODM/BRE:

`30_IBM_ODM_KNOWLEDGE/30_IBM_DOCUMENTATION_PROTOCOL.md`

`30_IBM_ODM_KNOWLEDGE/31_TARGET_PROFILE_E_PACKAGE_CLASSES.md`

`30_IBM_ODM_KNOWLEDGE/32_ODM_ARTIFACT_CATALOG.md`

`30_IBM_ODM_KNOWLEDGE/33_ODM_ARTIFACT_MAPPING_SPEC.md`

`30_IBM_ODM_KNOWLEDGE/34_CONSTRUCT_SUPPORT_MATRIX.md`

`30_IBM_ODM_KNOWLEDGE/35_EXECUTION_SEMANTICS_SPEC.md`

`30_IBM_ODM_KNOWLEDGE/36_EXPORT_COMPATIBILITY_SPEC.md`

---

## 4. Guard-rails invioláveis

Durante toda esta sessão, obedeça rigorosamente:

1. Não implementar antes de concluir bootstrap, repo discovery, leitura das fontes primárias, leitura dos contratos de orquestração e verificação dos gates.
2. Não tratar Prompt Library, Stage Cards, playbooks, ledgers ou relatórios históricos como fonte primária.
3. Não editar ZIP ou artefato ODM diretamente como fluxo principal.
4. Não propor mudança arquitetural sem indicar necessidade de ADR.
5. Não declarar comportamento IBM ODM/BRE por inferência.
6. Não declarar equivalência por outputs iguais.
7. Não fundir Execution Semantics e ODM Simulator.
8. Não fundir Structural Dependency Graph e Behavioral Dependency Graph.
9. Não fundir Behavior Discovery e Behavioral Knowledge.
10. Não transformar Simulator em fonte de comportamento real.
11. Não assumir domínio de negócio específico sem evidência.
12. Não abrir PR intermediário.
13. Não criar branch adicional sem autorização explícita da sessão mãe.
14. PR final, quando existir, só pode ser conduzido pela sessão mãe, após acceptance, gates e Devin Review.
15. Toda conclusão deve preservar Requirement → Evidence.
16. Toda lacuna deve ser classificada com status canônico apropriado.
17. Se a documentação interna responder à dúvida, use a documentação interna.
18. Se a documentação interna não responder uma dúvida técnica/IBM ODM/repo-specific, registre a lacuna e só então indique necessidade de fonte externa, repo discovery, IBM Docs, ODM real, SME review ou ADR.

---

## 5. O que você deve produzir nesta primeira resposta

Sua primeira resposta deve ser um relatório operacional estruturado com as seções abaixo.

### 5.1. Raiz documental encontrada

Informe:

- caminho da raiz documental encontrada;
- se ela corresponde à raiz esperada;
- arquivos obrigatórios encontrados;
- arquivos obrigatórios ausentes, se houver.

### 5.2. Decisão final da documentação

Com base nos arquivos da C8, informe:

- decisão final: `GO`, `GO_CONDICIONADO` ou `NO_GO`;
- existência ou ausência de P0/P1 aberto;
- existência ou ausência de P2 residual;
- restrições que continuam obrigatórias para o Devin.

### 5.3. Fontes lidas e autoridade

Liste:

- fontes primárias lidas;
- contratos de orquestração lidos;
- documentos derivados lidos;
- documentos históricos lidos apenas como evidência;
- qualquer conflito de autoridade encontrado.

### 5.4. Estado operacional inicial

Informe:

- se a documentação está apta para implementação real;
- se a sessão atual pode continuar como sessão mãe;
- se ainda há blocker documental;
- se há necessidade de ADR antes da primeira frente;
- se há necessidade de repo discovery antes da primeira frente.

### 5.5. Primeiras frentes elegíveis

Com base no Roadmap, DAG, Matrix, Gates e Global Unlock Matrix, proponha as primeiras frentes/stages elegíveis.

Para cada frente, informe:

- stage ou área;
- objetivo;
- por que está elegível;
- dependências;
- blockers;
- artefatos esperados;
- gates aplicáveis;
- riscos principais;
- se pode ser paralelizada ou não.

### 5.6. Primeira sessão dedicada recomendada

Escolha apenas uma primeira sessão dedicada segura.

Descreva:

- nome da sessão;
- objetivo;
- escopo autorizado;
- arquivos que deve consultar;
- arquivos que pode alterar;
- arquivos que não pode alterar;
- outputs esperados;
- critérios de aceite;
- handoff obrigatório;
- validações mínimas;
- blockers esperados;
- status recomendado: `GO`, `GO_CONDICIONADO`, `NO_GO` ou `NEEDS_REVIEW`.

### 5.7. Handoff esperado da primeira sessão dedicada

Defina o handoff que a sessão dedicada deverá devolver para a sessão mãe.

O handoff deve incluir, no mínimo:

- objetivo executado;
- arquivos consultados;
- arquivos alterados;
- evidências;
- decisões tomadas;
- decisões não tomadas;
- blockers;
- ADRs necessários;
- lacunas IBM ODM/BRE;
- validações executadas;
- resultado das validações;
- impacto em downstream;
- artifacts produzidos;
- status final;
- recomendação para unlock ou não unlock.

### 5.8. Decisão da sessão mãe

Finalize com uma decisão objetiva:

`GO` — pode iniciar a primeira sessão dedicada proposta.

`GO_CONDICIONADO` — pode iniciar apenas com condições explícitas.

`NO_GO` — não iniciar implementação.

`NEEDS_REVIEW` — precisa revisão humana antes de avançar.

Explique a decisão em termos de evidência documental, não de suposição.

---

## 6. Proibição de resposta genérica

Não responda com frases genéricas como:

- “vou analisar a documentação”;
- “parece tudo pronto”;
- “podemos começar implementando”;
- “vou seguir o guia”;
- “a arquitetura parece clara”.

Sua resposta deve demonstrar que você localizou os arquivos, entendeu a hierarquia documental, validou a decisão C8, leu os gates e escolheu a primeira frente com base em evidência.

Se não conseguir localizar ou ler os arquivos exigidos, pare e emita `NO_GO` ou `NEEDS_REVIEW`, explicando exatamente o que faltou.

---

## 7. Regra final

Esta primeira sessão não deve produzir código.

Ela deve produzir apenas a **preparação operacional segura** para que a sessão mãe possa abrir ou orientar a primeira sessão dedicada de implementação sem violar a documentação, os gates, os handoffs, os guard-rails IBM ODM/BRE, o workflow Git/PR e a rastreabilidade Requirement → Evidence.
