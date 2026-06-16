# PROMPT-MESTRE — Devin Repo Architecture Investigation
## Motor BAL maduro inutilizado vs Parser BAL deficitário no DLM / Estratégia arquitetural para preparar o repo para a arquitetura-alvo ODM V7

**Versão:** `V5_SESSION_MOTHER_ORCHESTRATOR_READY / LARGE_REPO_MULTI_SESSION / IMPLEMENTATION_QUALITY_AUDIT / MAX_QUALITY_EFFICIENCY / NO_IMPLEMENTATION_YET`

## Papel do Devin

Atue como:

- arquiteto de software sênior;
- repo investigator;
- revisor crítico de design;
- especialista em parsing/AST/semantic model/intermediate representation;
- especialista em arquitetura orientada a contratos;
- especialista em clean architecture, ports/adapters, anti-corruption layer, adapters, strategy, façades, dependency inversion, bounded contexts, lifecycle de artifacts e testability;
- agente de engenharia responsável por descobrir o estado real do repositório antes de propor qualquer implementação.

Sua missão é investigar e resolver arquiteturalmente, da melhor forma possível, o gap atual:

```text
Existe ou foi criado um motor BAL mais maduro/robusto.
Porém, o gerador de testes ainda consome o parser BAL antigo/deficitário acoplado ao DLM.
Integrar o motor BAL maduro diretamente ao DLM atual foi considerado complexo e arquiteturalmente difícil.
Isso ameaça a qualidade do gerador de testes, a cobertura por constructs e a prontidão do repo para implementar a arquitetura-alvo ODM V7.
```

A tarefa NÃO é fazer um remendo rápido.  
A tarefa é descobrir o estado real, entender a causa arquitetural, propor alternativas e recomendar a melhor estratégia para o bem maior do projeto.

---

## Objetivo final

Produzir uma análise arquitetural completa, evidence-driven e orientada a decisão para responder:

```text
Qual é a melhor forma arquitetural de eliminar o gap entre o motor BAL maduro, o parser BAL antigo do DLM e o gerador de testes, preservando a arquitetura-alvo ODM V7, evitando acoplamento indevido, evitando legado novo, evitando overengineering e preparando o repo para uma implementação limpa, testável, extensível e robusta?
```

A saída final deve permitir ao owner decidir entre opções como:

```text
1. substituir o parser antigo por trás de uma interface/port;
2. adaptar o motor BAL ao DLM por uma camada anticorrupção;
3. criar uma BAL Semantic Projection intermediária;
4. refatorar o DLM para receber semantic nodes/opaque nodes/support_status;
5. permitir consumo controlado do motor BAL por Coverage/Scenario via contrato;
6. manter temporariamente o parser antigo com diagnostics explícitos e plano de descontinuação;
7. outra alternativa superior encontrada no repo.
```

---

## Contexto arquitetural obrigatório

Use como referência a documentação-alvo ODM V7 anexada ou presente no projeto:

```text
ODM_V7_DOCUMENTACAO_UNIFICADA_IMPLEMENTATION_PLAN_READY.md
```

Princípios que NÃO podem ser violados sem `NEEDS_ADR / NEEDS_OWNER_REVIEW`:

```text
Canonical ODM Model é a fonte única editável corrente das regras.
DLM, Type System, Scenario Pack, Workbook, Export Bundle e Devin Index são derivados/views, salvo decisão primária explícita.
Mudanças em regra devem mirar o Canonical ODM Model, não derivados.
Derived artifacts devem ser reconstruídos ou invalidados, não editados como fonte.
Coverage/Testes deve ser construct-aware e evidence-gated.
Scenario Pack não pode virar truth store.
Simulator gera candidate_expected_output, nunca truth.
candidate_expected_output só vira verified_expected_output por Promotion Gate.
PASS_OBSERVABLE_MATCH não prova full behavioral equivalence, importability ou publish readiness.
Workbook é terminal; workbook_content é forbidden source.
Devin Index é metadata/evidence lookup, não autoridade.
Claims de repo exigem repo discovery com path, hash, comando ou evidência equivalente.
Claims IBM ODM/BRE exigem IBM docs, execução real, SME review, report, teste ou blocker explícito.
```

---

## Problema a investigar

O problema relatado é:

```text
O parser BAL antigo usado pelo DLM cobre poucos constructs.
Um motor BAL mais maduro foi criado para ampliar/amadurecer parsing/entendimento BAL.
Porém o motor BAL maduro não está no caminho crítico do gerador de testes.
O gerador de testes segue consumindo o parser antigo do DLM.
Integrar o motor BAL maduro ao DLM atual é considerado complexo e arquiteturalmente difícil.
```

A investigação deve verificar se isso é verdade no repo e, se for, medir o impacto.

---

## Hipótese arquitetural inicial

Trate como hipótese, não conclusão:

```text
O repo pode estar sofrendo de uma divergência entre capability implementada e capability efetivamente consumida.

Motor BAL maduro = capability técnica potencialmente melhor.
Parser antigo do DLM = producer real do gerador de testes.
Gerador de testes = consumer de uma representação possivelmente incompleta.

Risco: false coverage.
Constructs não parseados pelo parser antigo podem não gerar obligations, cenários, simulação, Real ODM observation, match ou diagnostics.
```

Essa hipótese precisa ser provada, refutada ou refinada por evidência do repo.

---

## Validação do prompt e princípios de instrução para sessão-mãe

Este prompt deve guiar uma **sessão-mãe-orquestradora**. Portanto, o Devin deve operar com disciplina de agente, e não como executor linear improvisado.

### Princípios obrigatórios de instrução de agente

```text
objetivo explícito;
escopo explícito;
fora de escopo explícito;
autoridade documental explícita;
proibições explícitas;
saídas obrigatórias;
fases com stop points;
sub-sessões com contexto delimitado;
evidência antes de conclusão;
separação entre fato, inferência, hipótese e recomendação;
Decision Ledger para decisões;
Evidence Ledger para fatos;
Conflict Ledger para divergências;
Requirement→Evidence para rastreabilidade;
GO/NO-GO por fase;
sem implementação antes de aprovação explícita;
sem conclusão global sem coverage map.
```

### Regra de sessão-mãe

A sessão-mãe deve:

```text
1. ler e preservar este prompt como contrato de execução;
2. criar work packages para sub-sessões;
3. impedir sub-sessões de expandirem escopo;
4. exigir evidence refs de cada sub-sessão;
5. consolidar sem apagar incertezas;
6. resolver conflitos por evidência, não por preferência;
7. manter status board e ledgers atualizados;
8. parar ao final de cada fase;
9. pedir comando explícito do owner para avançar.
```

A sessão-mãe não deve:

```text
executar implementação funcional;
permitir que uma sub-sessão altere código;
permitir que uma sub-sessão decida arquitetura sozinha;
aceitar “parece” como evidência;
aceitar “é complexo” como diagnóstico;
aceitar amostragem fraca como cobertura do repo;
compactar findings críticos em resumo genérico;
confundir current state com target state;
confundir workaround com arquitetura recomendada.
```

### Template obrigatório para work package de sub-sessão

Cada sub-sessão deve receber um pacote de trabalho neste formato:

```text
workstream_id:
título:
objetivo:
escopo_incluído:
escopo_excluído:
paths_alvo:
termos_de_busca:
comandos_autorizados:
artefatos_a_ler:
artefatos_a_produzir:
questões_obrigatórias:
critérios_de_evidência:
stop_conditions:
formato_de_handoff:
```

### Template obrigatório de handoff de sub-sessão

Cada sub-sessão deve devolver:

```text
workstream_id:
status = DONE | BLOCKED | PARTIAL | NEEDS_FOLLOW_UP
paths_inspecionados:
paths_relevantes_não_inspecionados:
comandos_executados:
achados_confirmados:
inferências:
unknowns:
blockers:
risks:
recommendations:
impacto_no_gap_BAL_DLM_GERADOR:
impacto_na_arquitetura_alvo_ODM_V7:
evidence_refs:
GO_NO_GO_local:
```

### Fato vs inferência vs recomendação

Toda afirmação deve ser marcada como uma destas categorias:

```text
FACT_REPO_EVIDENCE
FACT_TEST_OUTPUT
FACT_DOCUMENTED_TARGET_ARCHITECTURE
OWNER_OR_DEVIN_ASSERTION
INFERENCE_FROM_EVIDENCE
HYPOTHESIS
RECOMMENDATION
UNKNOWN
```

### Princípio de eficiência real

Eficiência, nesta investigação, significa:

```text
analisar menos contexto por vez;
gerar mais evidência reutilizável;
reduzir retrabalho por ledgers;
reduzir alucinação por workstreams pequenos;
paralelizar sem perder rastreabilidade;
consolidar por síntese evidence-backed.
```

Eficiência não significa:

```text
pular shards difíceis;
ignorar testes;
ignorar código legado;
concluir por nomes de arquivos;
implementar antes de entender;
aceitar solução que apenas funciona mas degrada arquitetura.
```

## Fidelidade arquitetural ODM V7 dentro da investigação

A investigação deve preservar a arquitetura-alvo como referência, mas deve separar claramente **estado atual do repo** de **arquitetura desejada**.

### Três planos de verdade

```text
1. Documentação-alvo ODM V7
   Decide princípios, boundaries, invariantes, target architecture e claims proibidos.

2. Repositório real
   Decide fatos físicos do estado atual: paths, classes, funções, comandos, testes, build, CI, fixtures e fluxo executável.

3. Evidência externa IBM/Real ODM
   Decide claims IBM-specific, runtime behavior, importability e observações comportamentais quando exigidas.
```

### Regra current vs target

Nunca misturar:

```text
CURRENT_STATE = o que o repo faz hoje;
TARGET_STATE = o que a arquitetura ODM V7 exige;
GAP = distância entre current e target;
RECOMMENDATION = caminho proposto para reduzir o gap;
IMPLEMENTATION = fora de escopo até aprovação explícita.
```

### Autoridade documental dentro do prompt

Se houver documentação ODM V7 no repo ou anexada, aplicar:

```text
1. Decision Ledger ou ADR aprovado mais recente, se existir e for aplicável.
2. 00_PROJECT_ESSENCE/
3. 20_ARCHITECTURE_CONTRACTS/
4. 30_IBM_ODM_KNOWLEDGE/
5. 10_ARCHITECTURE_OVERVIEW/
6. 40_DAG_AND_ROADMAP/
7. 60_IMPLEMENTABLE_ELEMENTS/
8. 50_ORCHESTRATORS/
9. 70_DEVIN_PLAYBOOKS/ e 80_PROMPT_LIBRARY/, apenas como execução derivada.
10. 45_LEGACY_MIGRATION_TO_TARGET/, apenas se escopo legacy for reaberto.
11. Código/repo real, somente para fatos físicos do estado atual.
12. Reports, prompts, summaries e handoffs, apenas como apoio/rastreabilidade.
```

### Regras de fidelidade ao V7

A recomendação final deve demonstrar aderência a:

```text
Canonical como fonte editável;
DLM/Type/Scenario/Workbook/Export/Index como derivados/views quando aplicável;
Patch/Invariant/Rebuild/Contract Validation como cadeia governada;
Coverage construct-aware e evidence-gated;
Scenario Pack como definition artifact;
Simulator candidate-only;
Promotion Gate para verified output;
PASS_OBSERVABLE_MATCH limitado a progressão até export;
Workbook terminal;
Devin Index metadata-only;
Export separado de Publish;
repo claims por discovery;
IBM claims por evidence.
```

Se qualquer recomendação exigir exceção, marcar:

```text
NEEDS_ADR
NEEDS_OWNER_REVIEW
NEEDS_DOC_PROPAGATION
```

### Anti-padrões específicos contra a documentação V7

Rejeitar ou marcar como `ARCHITECTURALLY_UNSAFE` qualquer opção que:

```text
faça o gerador de testes consumir internals do motor BAL sem contrato;
bypasse DLM/Canonical governance sem ADR;
faça DLM virar god object;
crie segundo source of truth para regras;
trate output do parser como coverage truth sem support_status;
omita construct unsupported/unknown;
trate parser antigo como suficiente sem negative tests;
acople export/publish a parsing/test generation;
transforme reports/workbook/index em fonte;
ignore lifecycle/rebuild/invalidation;
ignore contract validation;
crie legado novo sem deprecation plan.
```

## Auditoria obrigatória da qualidade da implementação atual

Além de investigar o gap específico entre motor BAL maduro, parser BAL antigo, DLM e gerador de testes, Devin deve realizar uma **auditoria aprofundada da qualidade arquitetural e implementacional do estado atual do repositório**.

Essa auditoria não deve ser genérica. Ela deve responder se as implementações atuais estão coerentes com:

```text
os princípios ODM V7;
a documentação-alvo ODM_V7_DOCUMENTACAO_UNIFICADA_IMPLEMENTATION_PLAN_READY.md;
clean architecture;
DDD quando aplicável;
ports/adapters;
dependency inversion;
contract-first design;
schema-first design;
producer/consumer clarity;
artifact lifecycle;
state machines claras;
separation of concerns;
low coupling / high cohesion;
testability;
observability;
maintainability;
evolvability;
anti-corruption layers;
design patterns adequados;
ausência de legado novo;
ausência de acoplamento acidental;
ausência de bypass de boundaries;
ausência de artifacts derivados tratados como fonte.
```

### Objetivo da auditoria de implementação

A auditoria deve permitir entender:

```text
1. quais partes do repo atual estão bem desenhadas e podem ser preservadas;
2. quais partes precisam apenas de adapters/contracts para se alinhar à arquitetura-alvo;
3. quais partes precisam de refactor;
4. quais partes devem ser substituídas;
5. quais partes estão criando acoplamento indevido com parser antigo, DLM, gerador de testes ou artifacts derivados;
6. quais partes dificultam o uso correto do motor BAL maduro;
7. quais problemas de qualidade tornam perigosa qualquer integração direta;
8. quais contratos, schemas, specs e builders precisam ser formalizados antes da implementação;
9. quais testes de caracterização e negative tests precisam ser criados para proteger a refatoração;
10. qual caminho de migração maximiza qualidade arquitetural e minimiza risco.
```

### Escopo mínimo da auditoria de qualidade

Auditar profundamente:

```text
camadas;
módulos/packages;
responsabilidades;
limites/boundaries;
ports/interfaces;
adapters;
builders;
parsers;
ASTs;
DLM;
projections;
schemas;
contracts;
DTOs/modelos intermediários;
artifact envelopes;
reports;
gates;
state/status enums;
lifecycle/invalidation;
coverage generator;
scenario/test generator;
simulator input/output contracts;
construct support matrix;
diagnostics/support_status;
source refs/lineage/hash;
tests;
fixtures;
CI/build commands;
error handling;
logging/observability;
configuração;
dependencies;
naming;
duplicação;
dead code;
legacy code;
coupling hotspots;
god classes/modules;
pass-through abstractions;
unowned artifacts.
```

### Critérios de avaliação por elemento

Para cada camada, módulo, builder, schema, contract ou artifact relevante, preencher:

```text
element_id:
path:
type = layer | module | builder | parser | model | schema | contract | artifact | report | gate | test | config
declared_or_inferred_responsibility:
actual_responsibility:
inputs:
outputs:
producers:
consumers:
source_of_truth_status:
derived_status:
contract_explicitness = explicit | implicit | missing | unclear
schema_status = versioned | unversioned | missing | not_applicable
boundary_quality = clear | leaky | violated | unknown
coupling_level = low | medium | high | critical
cohesion_level = high | medium | low | unclear
test_coverage = strong | partial | weak | missing | unknown
diagnostics_support = strong | partial | weak | missing
observability = strong | partial | weak | missing
alignment_with_odm_v7 = aligned | partially_aligned | misaligned | unknown
architectural_smell:
risk:
recommendation = KEEP | KEEP_AND_WRAP | ADAPT | REFACTOR | REPLACE | DEPRECATE | REMOVE | DEFER | NEEDS_REVIEW
evidence:
```

### Smells e anti-patterns a procurar

Procurar explicitamente:

```text
god object / god module;
parser internals leaking into consumers;
test generator coupled to old parser internals;
DLM trying to represent too much;
DLM too weak to represent required semantics;
motor BAL bypassing canonical/DLM governance;
duplicate parsing models without contract;
implicit contracts;
unversioned schemas;
stringly-typed domain;
missing diagnostics;
unsupported constructs dropped silently;
unknown constructs treated as success;
derived artifacts acting as source;
builders with mixed responsibilities;
reports used as gates;
state/status ambiguity;
hardcoded construct behavior;
framework leakage into domain;
business rules embedded in adapters;
copy-paste construct handling;
dead compatibility shims;
legacy parser kept without deprecation plan;
lack of characterization tests;
lack of negative tests;
lack of source refs/lineage/hash;
lack of rollback/migration plan;
overengineered abstractions without consumer value;
underengineered contracts around critical boundaries.
```

### Matriz obrigatória de qualidade da implementação

Produzir uma matriz consolidada:

```text
element
path
current_quality_score_0_to_5
odm_v7_alignment_score_0_to_5
coupling_risk
cohesion_risk
contract_risk
schema_risk
testability_risk
maintainability_risk
impact_on_bal_engine_integration
impact_on_test_generator_reliability
recommended_action
priority = P0 | P1 | P2
evidence
```

### Relação com o problema Motor BAL ↔ DLM ↔ Gerador

A auditoria de qualidade deve responder explicitamente:

```text
A implementação atual dificulta a integração do motor BAL por causa de qual problema arquitetural?
- DLM_EXPRESSIVENESS_GAP?
- PARSER_ENGINE_CONTRACT_GAP?
- TEST_GENERATOR_COUPLING?
- MISSING_SEMANTIC_PROJECTION?
- MISSING_ANTI_CORRUPTION_LAYER?
- MISSING_SUPPORT_STATUS_MODEL?
- MISSING_OPAQUE_NODE_STRATEGY?
- MISSING_TYPE_SYSTEM_BINDING?
- MISSING_LINEAGE_AND_DIAGNOSTICS?
- LEGACY_COMPATIBILITY_CONSTRAINT?
- ACCIDENTAL_COMPLEXITY?
- baixa qualidade de camada/builder/schema/contract?
```

A resposta deve identificar **qual refatoração melhora a qualidade do repo como um todo**, não apenas qual mudança “faz o motor BAL funcionar”.

### Saídas obrigatórias adicionais

Além dos reports já definidos, gerar:

```text
IMPLEMENTATION_QUALITY_AUDIT_REPORT.md
LAYER_BOUNDARY_INTEGRITY_REVIEW.md
SCHEMA_CONTRACT_SPEC_QUALITY_REVIEW.md
BUILDER_AND_ARTIFACT_QUALITY_REVIEW.md
CURRENT_IMPLEMENTATION_SMELL_REGISTER.md
CURRENT_IMPLEMENTATION_REFACTOR_CANDIDATE_MATRIX.md
ARCHITECTURAL_FIT_FOR_BAL_ENGINE_INTEGRATION.md
```

### Regra de recomendação

Nenhuma recomendação arquitetural final pode ser aceita sem responder:

```text
Essa opção melhora ou piora a qualidade arquitetural geral do repo?
Ela reduz acoplamento?
Ela melhora contracts/schemas?
Ela reduz false coverage?
Ela preserva boundaries?
Ela evita criar legado novo?
Ela melhora testabilidade?
Ela permite migração incremental?
Ela prepara o repo para a arquitetura-alvo ODM V7?
```

Se a opção apenas “funciona”, mas piora a arquitetura, classificar como:

```text
REJECTED_WORKS_BUT_ARCHITECTURALLY_UNSAFE
```


## Protocolo obrigatório de autonomia da sessão-mãe

Esta investigação deve ser conduzida em modo **orquestrador autônomo**.

O Devin deve avançar sozinho por fases, ondas, sub-sessões, workstreams, cross-checks, red team e consolidação final, sem pedir confirmação do owner a cada etapa.

### Regra central

```text
Não pedir permissão para avançar fase.
Não pedir permissão para abrir sub-sessão/workstream.
Não pedir permissão para executar buscas, leitura de arquivos, análise estática, testes de caracterização não destrutivos ou comandos read-only.
Não pedir confirmação para continuar quando houver apenas dúvida comum, lacuna parcial ou achado não crítico.
Continuar autonomamente e registrar dúvidas/gaps com labels.
```

### O que o Devin deve fazer autonomamente

O Devin deve, sem aguardar autorização humana:

```text
executar Fase 0 até Fase 8;
criar sessão-mãe/orquestradora;
criar sub-sessões/workstreams úteis;
dividir shards grandes em shards menores;
executar discovery read-only;
executar buscas estruturadas;
inspecionar código;
inspecionar testes;
inspecionar schemas/contracts/builders/specs;
executar comandos seguros e não destrutivos de build/test/lint quando disponíveis;
produzir reports parciais;
atualizar status board;
atualizar evidence ledger;
abrir conflict ledger;
abrir follow-up workstreams;
realizar cross-shard validation;
realizar red team;
produzir síntese final;
produzir ADR draft;
produzir plano de implementação futuro.
```

### Autonomia não significa implementar

Mesmo em modo autônomo, continua proibido:

```text
implementar código;
alterar código;
refatorar;
substituir parser;
alterar DLM;
conectar motor BAL ao gerador;
alterar documentação primária;
aplicar ADR;
executar comandos destrutivos;
alterar dados/fixtures sem autorização explícita;
commitar/pushar mudanças;
criar PR de implementação.
```

A autonomia é para **investigação, análise, auditoria, planejamento e recomendação**, não para mudança funcional.

### Quando parar e pedir intervenção do owner

O Devin só deve parar e pedir intervenção se houver impeditivo grave, como:

```text
BLOCKER_ACCESS_REPO
sem acesso ao repo ou branch correta;

BLOCKER_MISSING_REQUIRED_SOURCE
documento essencial ausente e impossível continuar com segurança;

BLOCKER_DESTRUCTIVE_ACTION_REQUIRED
a próxima ação necessária seria destrutiva, alteraria arquivos, mudaria dados, rodaria migração ou exigiria credencial sensível;

BLOCKER_SECURITY_OR_CREDENTIALS
necessidade de segredo, credential, token, ambiente protegido ou acesso sensível;

BLOCKER_AMBIGUOUS_OWNER_DECISION
duas ou mais opções arquiteturais têm trade-offs estratégicos equivalentes e exigem decisão de negócio/owner;

BLOCKER_INSUFFICIENT_EVIDENCE_FOR_DECISION
após discovery suficiente, ainda falta evidência crítica para recomendar arquitetura sem risco alto;

BLOCKER_CONTRADICTORY_EVIDENCE
evidências relevantes entram em conflito e não podem ser resolvidas por inspeção adicional;

BLOCKER_REAL_ODM_OR_IBM_DOCS_REQUIRED
a conclusão depende de IBM docs/Real ODM validation que não estão disponíveis;

BLOCKER_UNSAFE_TO_CONTINUE
continuar poderia gerar conclusão enganosa, false coverage ou recomendação arquitetural perigosa.
```

### O que não é blocker para parar

Não parar por:

```text
arquivo ainda não analisado mas não crítico;
lacuna parcial;
dúvida comum;
finding médio/baixo;
necessidade de criar mais sub-sessões;
necessidade de rodar mais buscas read-only;
necessidade de dividir shard;
necessidade de produzir mais um report;
ausência de evidência não crítica;
complexidade alta, desde que possa ser particionada.
```

Nesses casos, continuar e registrar:

```text
PENDENTE
NEEDS_REPO_DISCOVERY
NEEDS_CODE_INSPECTION
NEEDS_TEST_EXECUTION
NEEDS_FOLLOW_UP
NEEDS_REVIEW
```

### Checkpoints internos

Ao final de cada fase, o Devin deve gerar o fechamento da fase, mas **não deve parar aguardando comando humano** se o status for:

```text
GO
GO_WITH_WARNINGS
GO_WITH_FOLLOW_UP
PARTIAL_GO
```

Deve continuar para a próxima fase autonomamente.

Só deve parar se o status for:

```text
NO_GO_BLOCKER
NO_GO_FOR_ARCHITECTURAL_DECISION
BLOCKED_OWNER_INPUT_REQUIRED
BLOCKED_ACCESS_REQUIRED
BLOCKED_UNSAFE_TO_CONTINUE
```

### Formato de checkpoint autônomo

Ao fim de cada fase, registrar:

```text
phase_id
phase_status
summary
reports_created
evidence_added
open_findings
blockers
decision = CONTINUE_AUTONOMOUSLY | STOP_OWNER_INPUT_REQUIRED
next_phase
```

Se `decision = CONTINUE_AUTONOMOUSLY`, seguir imediatamente para a próxima fase.

### Regra final de autonomia

A sessão-mãe deve assumir responsabilidade por gerenciar o fluxo completo:

```text
planejar;
particionar;
executar;
consolidar;
validar;
red-team;
recomendar.
```

O owner não deve ser usado como scheduler de fases.  
O owner só deve ser acionado para decisões estratégicas reais ou impedimentos graves.


## Escopo obrigatório: somente implementação da arquitetura-alvo V7

Esta investigação deve ser feita **exclusivamente sobre as implementações relacionadas à arquitetura-alvo ODM V7**.

O Devin NÃO deve auditar, refatorar, analisar profundamente ou propor melhorias para a parte legada do repositório, salvo quando isso for estritamente necessário para:

```text
identificar fronteiras entre legado e target V7;
provar que um componente legado está sendo consumido pelo fluxo target V7;
medir risco de contaminação legado → target;
identificar dependência legada bloqueante;
planejar isolamento/depreciação futura;
evitar que a arquitetura-alvo seja construída sobre código legado frágil;
documentar que determinado módulo está OUT_OF_SCOPE
OUT_OF_SCOPE_LEGACY.
```

### Regra central

```text
Objeto da análise = implementações da arquitetura-alvo V7.

Código legado = OUT_OF_SCOPE, exceto quando cruza o caminho crítico da arquitetura-alvo V7.
```

### Como tratar parser antigo/DLM se forem legado

Se o parser BAL antigo, o DLM atual ou o gerador atual estiverem em código legado, o Devin deve aplicar esta regra:

```text
Não auditar o legado inteiro.
Não melhorar legado por conta própria.
Não propor refactor amplo de legado.

Analisar apenas:
1. se esse código legado está no caminho crítico do target V7;
2. qual contrato/dependência ele impõe ao target V7;
3. quais constructs ele omite;
4. qual risco ele cria para false coverage;
5. qual estratégia de isolamento, adapter, strangler, depreciação ou substituição é necessária para a arquitetura-alvo V7.
```

### O que está dentro do escopo

Incluir apenas elementos que sejam, comprovadamente, parte do target V7 ou consumidores/producers diretos da arquitetura-alvo:

```text
Canonical ODM Model target;
Patch Protocol / Patch Executor target;
DLM target ou DLM usado pelo target;
BAL engine target;
adapters/projections target;
Coverage/Test Planning target;
Coverage Obligation Model target;
Scenario Pack target;
Scenario/test generator target;
Simulator target;
Real ODM Observation target;
Observable Match target;
Promotion Gate target;
Workbook metadata boundary target;
Devin Index metadata-only target;
Export/Publish/ZIP target;
schemas/contracts/artifact envelopes target;
status namespaces target;
builders target;
orchestrators target;
tests target ligados à arquitetura V7;
CI/build commands necessários para validar target V7.
```

### O que está fora de escopo

Marcar como `OUT_OF_SCOPE_LEGACY` e não aprofundar, salvo dependência direta do target V7:

```text
legacy generator;
legacy expected output pipeline;
legacy migration code;
legacy-only parser paths;
legacy-only reports;
legacy-only workbook flows;
legacy-only export flows;
legacy-only XOM/BOM/JAR flows;
legacy test fixtures sem consumo pelo target V7;
legacy documentation não usada pelo target V7;
qualquer módulo sem relação demonstrada com a arquitetura-alvo V7.
```

### Regra de triagem target vs legacy

Antes de analisar profundamente qualquer arquivo/módulo, classificar:

```text
TARGET_V7_CORE
TARGET_V7_SUPPORTING
TARGET_V7_ADAPTER
TARGET_V7_TEST
TARGET_V7_DEPENDS_ON_LEGACY
LEGACY_TOUCHPOINT_FOR_TARGET
LEGACY_OUT_OF_SCOPE
UNKNOWN_NEEDS_CLASSIFICATION
```

Critérios:

```text
TARGET_V7_CORE
= implementa diretamente uma responsabilidade da arquitetura-alvo V7.

TARGET_V7_SUPPORTING
= support code necessário para target V7, mas não core.

TARGET_V7_ADAPTER
= adapter/ACL/projection/boundary entre target V7 e outro sistema/modelo.

TARGET_V7_TEST
= teste/fixture/contract test necessário para target V7.

TARGET_V7_DEPENDS_ON_LEGACY
= target V7 consome código legado; precisa de boundary/deprecation/strangler analysis.

LEGACY_TOUCHPOINT_FOR_TARGET
= legado não é alvo, mas toca target V7 e precisa ser mapeado para controle de risco.

LEGACY_OUT_OF_SCOPE
= não analisar além de registrar exclusão.

UNKNOWN_NEEDS_CLASSIFICATION
= não aprofundar até classificar.
```

### Saída obrigatória de triagem

Gerar:

```text
TARGET_V7_SCOPE_CLASSIFICATION.md
LEGACY_EXCLUSION_LEDGER.md
TARGET_LEGACY_TOUCHPOINT_RISK_REGISTER.md
```

Com matriz:

```text
path_or_module
classification
reason
target_v7_relationship
legacy_relationship
analyze_depth = full | boundary_only | exclude | unknown
risk_if_wrongly_included
risk_if_wrongly_excluded
evidence
```

### Regra anti-dispersão

Se uma sub-sessão começar a analisar legado que não tem relação comprovada com target V7, a sessão-mãe deve interromper essa sub-sessão e registrar:

```text
STOP_LEGACY_OUT_OF_SCOPE
```

### Regra para recomendações

A recomendação final deve focar em:

```text
como preparar o repo para a arquitetura-alvo V7;
como eliminar dependências legadas do caminho crítico V7;
como isolar touchpoints legados;
como deprecar parser antigo se ele for legado e estiver contaminando target V7;
como evitar construir arquitetura nova em cima de código legado frágil;
como garantir que o motor BAL robusto seja integrado por contrato limpo, adapter/projection ou outra estratégia target-compatible.
```

É proibido recomendar:

```text
melhorar legado por melhorar;
refatorar legado amplo fora do caminho V7;
migrar legado inteiro sem necessidade;
usar legado como source of truth;
criar novo código target acoplado a modelo legado;
preservar parser legado silenciosamente no target V7 sem diagnostics/deprecation plan.
```


## Protocolo obrigatório para repositório grande

Como o repositório possui muito código, esta investigação **não deve tentar analisar tudo em uma única sessão, nem em uma única passagem ampla e superficial**.

A investigação deve ser dividida em muitas sessões, sub-sessões e workstreams menores, com contexto restrito, foco claro, evidência rastreável e síntese posterior pela sessão-mãe.

O objetivo é:

```text
maximizar qualidade;
evitar baixa eficiência;
evitar alucinação;
evitar perda de contexto;
evitar conclusões por amostragem fraca;
evitar análise superficial;
evitar ignorar módulos importantes;
separar descoberta ampla de análise profunda;
permitir validação cruzada;
gerar rastreabilidade real por path/comando/evidência.
```

### Princípio central

```text
Nunca usar “repo muito grande” como justificativa para análise superficial.

Repo grande exige:
1. indexação;
2. particionamento;
3. análise por fatias;
4. ledgers de evidência;
5. síntese incremental;
6. cross-checks;
7. red team;
8. consolidação final.
```

### Estratégia obrigatória: breadth-first → shard → depth-first → cross-check

A investigação deve seguir esta estratégia:

```text
1. Breadth-first inventory:
   mapear rapidamente estrutura geral do repo, módulos, packages, build files, tests e entrypoints.

2. Sharding:
   dividir o repo em fatias pequenas e coerentes por domínio, camada, package, artifact ou fluxo.

3. Depth-first analysis:
   analisar profundamente cada fatia em sub-sessão própria.

4. Cross-shard validation:
   comparar achados entre fatias para encontrar inconsistências, duplicações, acoplamentos e contratos implícitos.

5. Synthesis:
   consolidar findings na sessão-mãe sem perder evidence refs.

6. Red team:
   atacar a conclusão com hipóteses adversariais antes do veredito final.
```

### Proibição de análise monolítica

É proibido:

```text
analisar o repo inteiro em uma única resposta;
tirar conclusão global sem inventory;
tirar conclusão global sem evidence ledger;
misturar parser, DLM, generator, simulator, export e tests na mesma análise profunda sem separar workstreams;
usar “não encontrei” sem documentar buscas/comandos;
usar apenas leitura de nomes de arquivos como prova de arquitetura;
assumir arquitetura por convenção de package;
concluir qualidade do repo sem inspecionar testes;
concluir integração sem dataflow/call graph;
concluir coverage sem construct matrix.
```

### Sharding mínimo obrigatório

A sessão-mãe deve dividir o repo, no mínimo, nestas fatias, sempre limitando a análise profunda ao que for target V7 ou touchpoint legado direto do target:

```text
SHARD-00 — repo/build/test/CI topology com classificação target-vs-legacy
SHARD-00A — target V7 scope classification e legacy exclusion ledger
SHARD-01 — rule sources / canonical / storage / fixtures
SHARD-02 — parser BAL antigo
SHARD-03 — motor BAL maduro
SHARD-04 — DLM core model
SHARD-05 — DLM builders/converters/projections
SHARD-06 — construct support / type system / diagnostics
SHARD-07 — coverage obligation generation
SHARD-08 — scenario/test generator
SHARD-09 — simulator input/output integration
SHARD-10 — Real ODM connector/observation, se existir
SHARD-11 — observable match/equivalence harness, se existir
SHARD-12 — promotion/expected outputs/fixtures
SHARD-13 — workbook/reports/HTML outputs
SHARD-14 — export/ZIP/XOM/BOM/JAR pipeline
SHARD-15 — contracts/schemas/artifact envelopes/status namespaces
SHARD-16 — tests/negative tests/characterization tests
SHARD-17 — observability/logging/errors/diagnostics
SHARD-18 — architecture smells/coupling/dead legacy
SHARD-19 — documentation/config/devin channels, se existirem
```

Se um shard for grande demais, subdividir novamente:

```text
SHARD-04A
SHARD-04B
SHARD-04C
...
```

ou:

```text
SS04-01
SS04-02
SS04-03
...
```

### Regra de tamanho de sub-sessão

Cada sub-sessão deve ter escopo pequeno o bastante para ser analisado profundamente.

Se uma sub-sessão precisar inspecionar muitos arquivos, ela deve se dividir em novas sub-sessões:

```text
Sub-sessão grande demais → dividir.
Mais de um domínio na mesma sub-sessão → dividir.
Mais de uma decisão arquitetural crítica na mesma sub-sessão → dividir.
Findings sem evidência suficiente → criar follow-up sub-sessão.
```

### Session budget protocol

Para cada sub-sessão, definir antes:

```text
scope;
non-goals;
target paths;
search terms;
commands;
expected outputs;
stop conditions;
handoff format.
```

A sub-sessão deve parar quando:

```text
atingir o escopo;
encontrar blocker;
precisar de outro shard;
precisar de evidence externa;
precisar de decisão do owner;
o contexto ficar amplo demais.
```

### Mapa de cobertura da investigação

A sessão-mãe deve manter um mapa:

```text
REPO_INVESTIGATION_COVERAGE_MAP.md
```

Com tabela:

```text
area_or_shard
status = NOT_STARTED | PARTIAL | COMPLETE | BLOCKED | NEEDS_FOLLOW_UP
paths_covered
paths_not_covered
commands_run
evidence_refs
confidence
remaining_risk
```

Nenhum relatório final pode dizer “repo analisado” sem listar o que foi coberto e o que não foi.

### Evidence-first rule para repo grande

Toda afirmação sobre o repo deve apontar para pelo menos um destes:

```text
path real;
símbolo/classe/função real;
comando executado;
teste executado;
resultado de busca;
call graph textual;
build/test output;
config/build file;
fixture real;
schema real;
report real;
hash/commit/branch quando aplicável.
```

Se não houver evidência, classificar como:

```text
INFERENCE
UNKNOWN
NEEDS_REPO_DISCOVERY
NEEDS_CODE_INSPECTION
NEEDS_TEST_EXECUTION
```

### Busca estruturada obrigatória

Antes das sub-sessões profundas, executar buscas estruturadas e registrar comandos para termos relacionados a:

```text
BAL
DLM
DecisionLogicModel
parser
parse
AST
engine
semantic
projection
builder
converter
rule
condition
action
construct
coverage
obligation
scenario
test generator
simulator
expected
fixture
promotion
observable
match
export
xom
bom
brl
schema
contract
status
diagnostic
unsupported
unknown
```

Adaptar termos à linguagem real do repo.

### Cross-check obrigatório

A sessão-mãe deve fazer cross-checks entre shards:

```text
Parser antigo vs Motor BAL maduro.
Motor BAL maduro vs DLM expressividade.
DLM builders vs Test Generator inputs.
Constructs reais vs constructs visíveis no generator.
Coverage obligations vs constructs unsupported/unknown.
Schemas/contracts declarados vs payloads reais.
Tests existentes vs risks encontrados.
Export/ZIP assumptions vs artifacts reais.
```

### Red team obrigatório para repo grande

Após análise dos shards, criar uma sub-sessão de red team que tente refutar a recomendação final:

```text
SS-REDTEAM — Challenge recommended architecture
```

Perguntas obrigatórias:

```text
A recomendação depende de arquivo não inspecionado?
A recomendação ignora módulo legado crítico?
A recomendação quebra consumidor oculto?
A recomendação aumenta acoplamento?
A recomendação cria novo modelo paralelo?
A recomendação transforma DLM em god object?
A recomendação deixa parser antigo vivo sem deprecation plan?
A recomendação permite false coverage?
A recomendação é big-bang demais?
A recomendação não tem testes suficientes?
```

### Checkpoint obrigatório antes de decisão final

Antes da Fase 6 ou qualquer ADR draft, a sessão-mãe deve produzir:

```text
PRE_DECISION_EVIDENCE_READINESS_CHECK.md
```

Com:

```text
áreas cobertas;
áreas não cobertas;
evidências fortes;
evidências fracas;
claims ainda inferidos;
blockers;
risco de decidir cedo demais;
GO/NO-GO para propor arquitetura recomendada.
```

Se houver risco alto de decisão prematura:

```text
NO_GO_FOR_ARCHITECTURAL_DECISION
```

### Regra de eficiência

Eficiência aqui significa:

```text
não repetir leituras desnecessárias;
não reabrir shards completos sem motivo;
não carregar contexto irrelevante;
usar summaries/handoffs para transferir contexto;
usar evidence ledger em vez de memória;
fazer síntese incremental;
criar follow-ups pequenos;
preservar decisões em decision ledger.
```

Eficiência NÃO significa:

```text
pular discovery;
pular testes;
pular arquivos difíceis;
pular módulos grandes;
concluir por amostragem fraca;
aceitar opinião sem evidência.
```

### Artefatos adicionais obrigatórios para repo grande

Gerar e manter:

```text
REPO_INVESTIGATION_COVERAGE_MAP.md
REPO_SEARCH_COMMAND_LOG.md
REPO_PATH_AND_SYMBOL_INDEX.md
REPO_SHARDING_PLAN.md
REPO_SHARD_HANDOFF_LEDGER.md
TARGET_V7_SCOPE_CLASSIFICATION.md
LEGACY_EXCLUSION_LEDGER.md
TARGET_LEGACY_TOUCHPOINT_RISK_REGISTER.md
PRE_DECISION_EVIDENCE_READINESS_CHECK.md
SS_REDTEAM_RECOMMENDATION_CHALLENGE.md
```


## Estratégia obrigatória de sessões e sub-sessões Devin

Esta investigação deve ser conduzida com o **máximo de paralelização analítica segura** que o Devin conseguir suportar.

O objetivo da divisão em sessões/sub-sessões **não é apenas ganhar tempo**. O objetivo principal é:

```text
maximizar qualidade analítica;
reduzir perda de contexto;
evitar análise superficial;
separar preocupações arquiteturais;
produzir evidências independentes;
permitir comparação cruzada;
evitar viés de uma única linha de raciocínio;
aumentar chance de detectar gaps, anti-patterns e false coverage;
preservar contexto ótimo por subproblema.
```

### Modelo obrigatório

Use uma sessão-mãe/orquestradora e múltiplas sub-sessões especializadas.

```text
Sessão-mãe / Orquestradora
→ define escopo;
→ distribui workstreams;
→ consolida evidências;
→ resolve conflitos entre sub-sessões;
→ mantém Decision Ledger;
→ produz síntese final;
→ não aceita conclusão sem evidence refs.

Sub-sessões especializadas
→ investigam áreas pequenas e profundas;
→ produzem reports próprios;
→ citam paths, comandos, testes e evidências;
→ declaram dúvidas, blockers e incertezas;
→ não implementam código;
→ não fazem mudanças funcionais.
```

Se o Devin não suportar sub-sessões reais, simule a divisão por **workstreams sequenciais isolados**, cada um com report próprio, contexto delimitado e checklist independente.

### Regra anti-perda de contexto

Cada sub-sessão/workstream deve produzir um handoff mínimo:

```text
workstream_id
escopo
arquivos inspecionados
comandos executados
achados
evidências
hipóteses descartadas
dúvidas abertas
risco arquitetural
impacto no plano ODM V7
recommendation
GO/NO-GO local
```

A sessão-mãe só pode consolidar uma conclusão se conseguir apontar para evidência de uma ou mais sub-sessões.

### Sub-sessões obrigatórias recomendadas

Crie o máximo possível de sub-sessões úteis, mas no mínimo estas:

| ID | Sub-sessão | Objetivo | Saída |
|---|---|---|---|
| SS-01 | Repo topology e inventory | Mapear módulos, packages, build system, entrypoints, testes e artefatos relacionados a BAL, DLM, gerador de testes, coverage, simulator e export. | `SS01_REPO_TOPOLOGY_AND_INVENTORY.md` |
| SS-02 | Parser BAL antigo | Descobrir implementação, contracts, inputs/outputs, constructs suportados, testes, diagnostics e consumidores do parser antigo. | `SS02_OLD_BAL_PARSER_REVIEW.md` |
| SS-03 | Motor BAL maduro | Descobrir arquitetura, modelo interno, AST/semantic model, constructs suportados, testes, diagnostics e readiness do motor BAL maduro. | `SS03_MATURE_BAL_ENGINE_REVIEW.md` |
| SS-04 | DLM model e expressividade | Avaliar se o DLM atual consegue representar constructs do motor BAL, se há semantic gap, opaque node strategy, support_status, source_refs, lineage e type binding. | `SS04_DLM_EXPRESSIVENESS_AND_MODEL_REVIEW.md` |
| SS-05 | Gerador de testes e coverage pipeline | Mapear exatamente o que o gerador consome, como gera cenários/coverage, se detecta unsupported/unknown e se pode produzir false coverage. | `SS05_TEST_GENERATOR_AND_COVERAGE_PIPELINE_REVIEW.md` |
| SS-06 | Construct inventory e regras reais | Inventariar constructs BAL/ODM presentes nas regras do projeto e comparar com parser antigo, motor BAL e DLM. | `SS06_REAL_RULE_CONSTRUCT_INVENTORY.md` |
| SS-07 | Contract/boundary analysis | Analisar producer/consumer contracts entre motor BAL, parser antigo, DLM, coverage generator, Scenario Pack, simulator e artifacts. | `SS07_CONTRACT_AND_BOUNDARY_ANALYSIS.md` |
| SS-08 | Architectural options | Avaliar opções: port/interface replacement, anti-corruption adapter, BAL Semantic Projection, DLM extensível, direct consumption, legacy-with-diagnostics, hybrid strangler. | `SS08_ARCHITECTURAL_OPTIONS_REVIEW.md` |
| SS-09 | Test strategy e negative tests | Definir characterization tests, contract tests, construct visibility tests e negative tests contra silent construct drop e false coverage. | `SS09_TEST_STRATEGY_AND_NEGATIVE_TESTS.md` |
| SS-10 | Risk, migration e rollback | Analisar riscos, plano incremental, backward compatibility, depreciação do parser antigo, rollback, shims e feature flags se aplicável. | `SS10_RISK_MIGRATION_ROLLBACK_REVIEW.md` |
| SS-19 | Auditoria de qualidade da implementação atual | Auditar camadas, artifacts, schemas, contracts, specs, builders, boundaries, tests, diagnostics, coupling/cohesion e aderência do repo aos princípios ODM V7 e boas práticas arquiteturais. | `SS19_IMPLEMENTATION_QUALITY_AUDIT.md` |

### Sub-sessões opcionais

Adicionar quando houver evidência ou complexidade suficiente:

```text
SS-11 — Performance/cost of mature BAL engine
SS-12 — Type System binding review
SS-13 — XOM/BOM/JAR impact review
SS-14 — IBM ODM docs/construct semantics review
SS-15 — Real ODM validation planning
SS-16 — Security/artifact poisoning/stale artifact risk review
SS-17 — Clean Architecture / DDD boundary review
SS-18 — Developer experience and maintainability review
```

### Ondas de execução recomendadas

```text
Wave 1 — Discovery paralelo:
SS-01, SS-02, SS-03, SS-04, SS-05, SS-06

Wave 2 — Análise cruzada:
SS-07, SS-08, SS-09, SS-10, SS-19

Wave 3 — Reviews opcionais:
SS-11 a SS-18 conforme necessidade

Wave 4 — Consolidação:
comparar achados;
resolver conflitos;
produzir root cause;
selecionar recomendação;
preparar ADR draft;
preparar implementation plan.
```

### Regra de comparação cruzada

A sessão-mãe deve cruzar obrigatoriamente:

```text
SS-02 parser antigo
vs SS-03 motor BAL maduro
vs SS-06 constructs reais
vs SS-05 visibilidade do gerador
```

para responder:

```text
quais constructs existem;
quais constructs o parser antigo enxerga;
quais constructs o motor BAL enxerga;
quais constructs o DLM representa;
quais constructs o gerador de testes transforma em coverage/scenario;
quais constructs são omitidos silenciosamente;
onde existe false coverage.
```

Também deve cruzar:

```text
SS-04 DLM expressividade
vs SS-07 contracts/boundaries
vs SS-08 options
```

para decidir se o melhor caminho é:

```text
adapter;
semantic projection;
DLM extensível;
parser port replacement;
hybrid strangler;
ou outra opção.
```

### Regra de conflito entre sub-sessões

Se duas sub-sessões chegarem a conclusões diferentes, a sessão-mãe deve abrir item no ledger:

```text
conflict_id
subsession_a_claim
subsession_b_claim
evidence_a
evidence_b
resolution
remaining_uncertainty
required_action
```

Não resolver conflito por preferência subjetiva.

### Regra de qualidade da recomendação final

A recomendação final só é aceitável se:

```text
não acoplar o gerador de testes a internals de parser;
não transformar o DLM em god object;
não bypassar Canonical/DLM governance sem ADR;
não manter o parser antigo como fonte silenciosa de false coverage;
não esconder unsupported/unknown constructs;
não criar legado novo;
não exigir big-bang refactor se houver caminho incremental seguro;
incluir contract tests e negative tests;
incluir plano de depreciação do parser antigo se aplicável;
incluir rollback/migration path;
incluir impacto na arquitetura-alvo ODM V7.
```

### Artefatos de orquestração obrigatórios

Além dos reports de fases, gerar:

```text
SUBSESSION_ORCHESTRATION_PLAN.md
SUBSESSION_STATUS_BOARD.md
SUBSESSION_EVIDENCE_LEDGER.md
SUBSESSION_CONFLICT_LEDGER.md
SUBSESSION_REQUIREMENT_EVIDENCE_INDEX.md
REPO_INVESTIGATION_COVERAGE_MAP.md
REPO_SEARCH_COMMAND_LOG.md
REPO_PATH_AND_SYMBOL_INDEX.md
REPO_SHARDING_PLAN.md
REPO_SHARD_HANDOFF_LEDGER.md
TARGET_V7_SCOPE_CLASSIFICATION.md
LEGACY_EXCLUSION_LEDGER.md
TARGET_LEGACY_TOUCHPOINT_RISK_REGISTER.md
PRE_DECISION_EVIDENCE_READINESS_CHECK.md
SS_REDTEAM_RECOMMENDATION_CHALLENGE.md
PARENT_ORCHESTRATOR_DECISION_LEDGER.md
SUBSESSION_WORK_PACKAGE_TEMPLATES.md
ARCHITECTURAL_DECISION_SYNTHESIS.md
```

### Status board obrigatório

Manter tabela:

```text
subsession_id
status = NOT_STARTED | RUNNING | DONE | BLOCKED | NEEDS_FOLLOW_UP
scope
owner/agent
inputs
outputs
key_findings
blockers
confidence
```

### Evidence ledger obrigatório

Toda evidência importante deve ser registrada:

```text
evidence_id
source_path
line_or_symbol_or_command
observed_fact
used_by_subsessions
supports_claims
limitations
```


## Regras de conduta

Não implemente código nesta investigação, salvo se o owner pedir explicitamente depois.

Não altere arquivos do repo, exceto criar reports Markdown de investigação.

Não crie refactor.

Não substitua parser.

Não altere DLM.

Não conecte motor BAL ao gerador de testes.

Não faça “quick fix”.

Não esconda complexidade.

Não aceite como verdade a afirmação “é difícil integrar” sem explicar tecnicamente por quê.

Não conclua que a melhor solução é integrar tudo no DLM sem comparar alternativas.

Não conclua que a melhor solução é o gerador consumir o motor BAL diretamente sem avaliar acoplamento e violação de boundaries.

Não preserve o parser antigo por conveniência se ele gera false coverage.

Não invente comportamento IBM ODM.

Não declare cobertura robusta se os constructs não forem evidenciados.

Não use resultado de testes atuais como prova de coverage se o parser consumido for deficitário.

---

## Critérios arquiteturais de qualidade

Avalie todas as opções contra:

```text
source of truth preservation;
single responsibility;
dependency inversion;
ports/adapters;
anti-corruption layer;
schema/contract clarity;
producer/consumer clarity;
bounded context;
testability;
extensibility for new constructs;
diagnostics/support_status;
lifecycle/rebuild/invalidation;
backward compatibility;
migration safety;
observability;
minimal coupling;
minimal accidental complexity;
no false coverage;
no silent construct omission;
readiness for ODM V7 architecture target;
cost/risk/benefit;
incremental delivery;
rollback/deprecation path.
```

Use também como benchmark conceitual:

```text
C4-style architecture views para mapear contexto/container/component/dataflow;
arc42-style structure para constraints, building blocks, runtime view, risks e decisions;
Well-Architected principles para operabilidade, confiabilidade, segurança, performance e evolução;
OWASP-style threat/data-flow thinking para artifact poisoning, stale artifacts, trust boundaries e tampering;
contract testing / schema-first mindset para validar producers/consumers.
```

---

## Labels obrigatórios

Use exatamente estes labels quando aplicável:

```text
NEEDS_REPO_DISCOVERY
NEEDS_CODE_INSPECTION
NEEDS_TEST_EXECUTION
NEEDS_CHARACTERIZATION
NEEDS_CONTRACT_MAPPING
NEEDS_ARCHITECTURAL_DECISION
NEEDS_ADR
NEEDS_OWNER_REVIEW
NEEDS_IBM_DOCS
NEEDS_REAL_ODM_VALIDATION
NEEDS_REFACTOR_PLAN
NEEDS_DEPRECATION_PLAN
NEEDS_NEGATIVE_TESTS
NEEDS_BACKWARD_COMPATIBILITY_PLAN
BLOCKER
PENDENTE
DEFERRED
OUT_OF_SCOPE
```

---

## Severidade obrigatória

Classifique findings com:

```text
CRITICAL
HIGH
MEDIUM
LOW
INFO
```

Use `CRITICAL` se houver omissão silenciosa de constructs que faça o gerador parecer cobrir regras que ele não entende.

---

## Definition of Done global da investigação

A investigação só pode ser considerada completa se existir:

```text
REPO_INVESTIGATION_COVERAGE_MAP.md atualizado;
SUBSESSION_STATUS_BOARD.md atualizado;
SUBSESSION_EVIDENCE_LEDGER.md atualizado;
SUBSESSION_CONFLICT_LEDGER.md, se houver conflitos;
CURRENT_STATE vs TARGET_STATE vs GAP claramente separados;
Construct visibility matrix;
Parser antigo vs motor BAL capability matrix;
DLM expressiveness diagnosis;
Test generator input-source diagnosis;
Implementation quality audit;
Architectural options matrix;
Pre-decision evidence readiness check;
ADR draft com status DRAFT / NEEDS_OWNER_REVIEW / NO_ADR_APPROVAL;
Plano incremental P0/P1/P2;
Validation gates e negative tests;
Handoff final para implementação futura.
```

Se qualquer item acima não for possível, registrar explicitamente:

```text
PARTIAL_COMPLETION
BLOCKED_BY_MISSING_EVIDENCE
NEEDS_FOLLOW_UP_SESSION
```

## Definição de qualidade mínima por decisão arquitetural

Nenhuma decisão arquitetural pode ser recomendada se não responder:

```text
Qual problema resolve?
Qual risco reduz?
Qual contrato cria ou preserva?
Qual boundary protege?
Qual acoplamento reduz?
Qual novo acoplamento introduz?
Qual custo de implementação?
Qual custo de manutenção?
Qual alternativa foi rejeitada e por quê?
Qual teste negativo protege contra regressão?
Qual plano de rollback/deprecation existe?
Qual impacto na arquitetura-alvo ODM V7?
Qual evidência sustenta a decisão?
```

# Fases obrigatórias

## Regra de execução autônoma

Execute autonomamente da Fase 0 até a Fase 8.

Não aguarde comando do owner entre fases.

Ao final de cada fase:

```text
registre fechamento da fase;
atualize ledgers;
classifique GO/NO-GO interno;
continue automaticamente se não houver blocker grave;
não implemente;
não altere código;
não altere documentação primária.
```

Sequência de execução esperada:

```text
Fase 0 — Status de entrada e plano de investigação.
Fase 1 — Repo discovery do fluxo BAL/DLM/Gerador.
Fase 2 — Matriz de capacidade parser antigo vs motor BAL vs regras reais.
Fase 3 — Dataflow, producers/consumers, contracts e boundaries.
Fase 4 — Diagnóstico arquitetural da causa-raiz.
Fase 5 — Opções arquiteturais e trade-offs.
Fase 6 — Estratégia recomendada e ADR draft.
Fase 7 — Plano de implementação incremental e validation gates.
Fase 8 — Pacote final de investigação e handoff.
```

Parar somente em caso de impeditivo grave conforme o protocolo de autonomia.

---

# Fase 0 — Status de entrada e plano de investigação

## Objetivo

Confirmar fontes, repo, branch, escopo, limitações e plano.

## Ações

1. Confirmar branch atual.
2. Confirmar se o repo está limpo.
3. Identificar linguagem/framework/build system.
4. Localizar documentação do projeto relevante.
5. Confirmar quais arquivos de arquitetura ODM V7 estão disponíveis.
6. Declarar que nenhuma implementação será feita nesta fase.
7. Definir estratégia de busca no repo.

## Produza

```text
00_BAL_DLM_INVESTIGATION_STATUS_AND_PLAN.md
```

## Deve conter

```text
repo/branch/status;
fontes recebidas;
fontes ausentes;
hipóteses iniciais;
escopo;
fora de escopo;
estratégia de repo discovery;
comandos que serão usados;
riscos iniciais;
GO/NO-GO para Fase 1.
```

---

# Fase 1 — Repo discovery do fluxo BAL/DLM/Gerador

## Objetivo

Descobrir o fluxo real de parsing BAL, DLM e geração de testes.

## Ações obrigatórias

Localizar e documentar:

```text
parser BAL antigo;
novo motor BAL;
DLM atual;
builders/converters para DLM;
gerador de testes;
coverage generator;
scenario generator;
simulator input builder;
construct support matrix, se existir;
test fixtures;
expected outputs;
commands de build/test;
CI pipeline relevante.
```

Executar buscas por termos como:

```text
BAL
DLM
DecisionLogicModel
parser
parse
engine
rule
condition
action
construct
scenario
coverage
test generator
simulator
xom
bom
brl
```

Adaptar termos conforme linguagem/framework do repo.

## Produza

```text
01_REPO_DISCOVERY_BAL_DLM_TEST_GENERATOR.md
IMPLEMENTATION_QUALITY_AUDIT_REPORT.md
LAYER_BOUNDARY_INTEGRITY_REVIEW.md
SCHEMA_CONTRACT_SPEC_QUALITY_REVIEW.md
BUILDER_AND_ARTIFACT_QUALITY_REVIEW.md
CURRENT_IMPLEMENTATION_SMELL_REGISTER.md
```

## Deve conter

```text
file/path inventory;
component map;
entrypoints;
call graph textual;
build/test commands;
evidence refs;
unknowns;
risks.
```

## Matriz obrigatória

```text
component
path
role
producer_of
consumer_of
entrypoint
tests
evidence_command
confidence
notes
```

---

# Fase 2 — Matriz de capacidade parser antigo vs motor BAL vs regras reais

## Objetivo

Comparar objetivamente o que cada parser/motor entende e o que as regras reais exigem.

## Ações obrigatórias

1. Inventariar constructs usados nas regras reais.
2. Inventariar constructs suportados pelo parser antigo.
3. Inventariar constructs suportados pelo motor BAL maduro.
4. Identificar constructs ignorados, parcialmente parseados, tratados como texto bruto, tratados como unsupported ou quebrados.
5. Verificar se há testes de parser para cada construct.
6. Verificar se há fixtures reais de regra cobrindo os constructs.
7. Verificar se o gerador de testes recebe diagnostics de unsupported/unknown.

## Produza

```text
02_BAL_CAPABILITY_AND_CONSTRUCT_VISIBILITY_MATRIX.md
```

## Matrizes obrigatórias

### Construct matrix

```text
construct
present_in_real_rules
old_parser_support = full | partial | none | unknown
bal_engine_support = full | partial | none | unknown
dlm_representation = explicit | opaque | text | missing | unknown
test_generator_visibility = visible | partial | invisible | unknown
coverage_obligation_generated = yes | no | partial | unknown
diagnostic_emitted = yes | no | unknown
risk
evidence
```

### Parser test matrix

```text
construct
old_parser_test
bal_engine_test
integration_test
negative_test
fixture
gap
```

## Veredito obrigatório

Classificar:

```text
NO_FALSE_COVERAGE_RISK
FALSE_COVERAGE_RISK_LOW
FALSE_COVERAGE_RISK_MEDIUM
FALSE_COVERAGE_RISK_HIGH
FALSE_COVERAGE_RISK_CRITICAL
```

---

# Fase 3 — Dataflow, producers/consumers, contracts e boundaries

## Objetivo

Mapear como dados saem das regras/BAL e chegam ao gerador de testes.

## Ações obrigatórias

Desenhar o dataflow real:

```text
rule source
→ parser antigo ou motor BAL
→ AST/parse result
→ DLM
→ coverage/test generator
→ scenario/test artifacts
→ simulator/expected output pipeline, se existir
```

Identificar:

```text
quem é producer;
quem é consumer;
qual contrato existe;
se o contrato é explícito ou implícito;
se há schemas;
se há versionamento;
se há diagnostics;
se há support_status;
se há opaque nodes;
se há source refs;
se há lineage/hash;
se há lifecycle/invalidation.
```

## Produza

```text
03_BAL_DLM_DATAFLOW_CONTRACT_BOUNDARY_MAP.md
```

## Matriz obrigatória

```text
edge
producer
consumer
payload_or_model
contract_explicitness
schema_or_type
versioning
diagnostics
support_status
lineage
risk
recommendation
```

## Red flags obrigatórias

Marcar se houver:

```text
implicit contract;
consumer depending on internal parser model;
DLM leaking parser internals;
test generator coupled to weak parser;
BAL engine not in critical path;
two competing parse models;
construct dropped silently;
unsupported not represented;
no diagnostics;
no lineage;
no negative tests.
```

---

# Fase 4 — Diagnóstico arquitetural da causa-raiz

## Objetivo

Explicar por que o motor BAL maduro não foi integrado ao DLM/gerador e qual é a causa arquitetural real.

## Perguntas obrigatórias

Responder com evidência:

```text
A dificuldade é técnica, conceitual ou acidental?
O DLM atual não tem expressividade?
O motor BAL expõe modelo semântico incompatível?
O DLM tenta representar detalhes demais?
O motor BAL foi implementado sem port/adapter?
O gerador de testes está acoplado ao parser antigo?
Falta contrato intermediário?
Falta support_status/opaque node?
Falta type system?
Falta source refs/lineage?
Falta test harness?
Há medo de quebrar compatibilidade?
Há ausência de owner/ADR?
```

## Produza

```text
04_ROOT_CAUSE_ARCHITECTURAL_DIAGNOSIS.md
```

## Classificar causa-raiz

Use uma ou mais:

```text
DLM_EXPRESSIVENESS_GAP
PARSER_ENGINE_CONTRACT_GAP
TEST_GENERATOR_COUPLING
MISSING_SEMANTIC_PROJECTION
MISSING_ANTI_CORRUPTION_LAYER
MISSING_SUPPORT_STATUS_MODEL
MISSING_OPAQUE_NODE_STRATEGY
MISSING_TYPE_SYSTEM_BINDING
MISSING_LINEAGE_AND_DIAGNOSTICS
LEGACY_COMPATIBILITY_CONSTRAINT
UNDERENGINEERED_DLM
OVERENGINEERED_BAL_ENGINE
ACCIDENTAL_COMPLEXITY
```

---

# Fase 5 — Opções arquiteturais e trade-offs

## Objetivo

Comparar alternativas e selecionar candidatas sérias.

## Opções mínimas a avaliar

Avaliar pelo menos:

```text
A. Replace behind interface:
   substituir o parser antigo por trás de uma ParserPort/BalParserPort, mantendo consumidores estáveis.

B. Anti-corruption adapter:
   motor BAL → adapter/ACL → DLM-compatible model.

C. BAL Semantic Projection:
   motor BAL → BAL_PARSE_RESULT / BAL_SEMANTIC_PROJECTION → DLM Input Projection / Coverage.

D. DLM extensível:
   refatorar DLM para explicit/opaque/unsupported semantic nodes, support_status, diagnostics e source refs.

E. Direct consumption by test generator:
   gerador consome motor BAL diretamente por contrato específico.

F. Legacy parser with diagnostics:
   manter parser antigo temporariamente, mas emitir unsupported/unknown/blockers e impedir false coverage.

G. Hybrid strangler:
   introduzir motor BAL por constructs gradualmente, com adapter e feature flags/contract tests.
```

## Produza

```text
05_ARCHITECTURAL_OPTIONS_AND_TRADEOFFS.md
```

## Matriz obrigatória

```text
option
description
pattern
benefits
risks
coupling_risk
complexity_cost
migration_cost
testability
compatibility
fit_to_odm_v7_target
false_coverage_mitigation
rollback_strategy
recommended_for
decision
```

## Critérios de decisão

A recomendação deve favorecer:

```text
baixo acoplamento;
contratos explícitos;
migração incremental;
diagnostics claros;
sem omissão silenciosa;
preservação do Canonical/DLM como cadeia governada;
evitar DLM god object;
evitar gerador de testes acoplado a parser internals;
evitar legado novo;
facilidade de testes negativos;
aderência à arquitetura-alvo ODM V7.
```

---

# Fase 6 — Estratégia recomendada e ADR draft

## Objetivo

Recomendar a solução arquitetural final e redigir um ADR draft.

## Produza

```text
06_RECOMMENDED_BAL_DLM_ARCHITECTURE_AND_ADR_DRAFT.md
```

## Deve conter

```text
veredito;
opção recomendada;
opções descartadas e por quê;
arquitetura alvo;
contratos propostos;
artifact boundaries;
dataflow alvo;
impacto em DLM;
impacto no gerador de testes;
impacto em Coverage Obligations;
impacto em Scenario Pack;
impacto em Simulator;
impacto em Contract Validation;
risco de compatibilidade;
migração incremental;
rollback/deprecation strategy;
ADR draft.
```

## ADR draft deve conter

```text
status = DRAFT / NEEDS_OWNER_REVIEW / NO_ADR_APPROVAL
context
problem
decision
considered_options
decision_drivers
consequences_positive
consequences_negative
migration_plan
validation_plan
open_questions
required_owner_decisions
```

---

# Fase 7 — Plano de implementação incremental e validation gates

## Objetivo

Criar plano de implementação futuro, sem executar implementação.

## Produza

```text
07_INCREMENTAL_IMPLEMENTATION_PLAN_AND_VALIDATION_GATES.md
```

## Plano mínimo

Separar em P0/P1/P2:

```text
P0 — Safety and discovery closure:
- bloquear false coverage;
- diagnostics de unsupported/unknown;
- tests que provam parser antigo não omite silenciosamente;
- mapping claro do fluxo atual.

P1 — Integration foundation:
- introduzir port/interface/adapter/projection;
- contract tests;
- DLM support_status/opaque nodes se recomendado;
- generator consumer migration behind contract.

P2 — Full maturation:
- deprecar parser antigo;
- ampliar construct support;
- integrar com coverage obligations/scenario/simulator;
- real ODM validation por construct/facet;
- remover compatibility shims.
```

## Validation gates obrigatórios

```text
no silent construct drop;
old parser vs engine capability delta visible;
unsupported/unknown blocks strong coverage;
test generator consumes contract, not parser internals;
Scenario Pack remains definition artifact;
DLM does not become god object;
BAL engine does not bypass Canonical governance;
contract validation catches mismatch;
migration is reversible;
```

---

# Fase 8 — Pacote final de investigação e handoff

## Objetivo

Consolidar tudo em um pacote final para owner/Devin/próxima sessão.

## Produza

```text
08_BAL_DLM_ARCHITECTURE_INVESTIGATION_FINAL_REPORT.md
BAL_DLM_ARCHITECTURE_REQUIREMENT_EVIDENCE.md
BAL_DLM_ARCHITECTURE_DECISION_LEDGER.md
BAL_DLM_ARCHITECTURE_IMPLEMENTATION_HANDOFF.md
```

Opcionalmente, se conveniente:

```text
BAL_DLM_ARCHITECTURE_INVESTIGATION_PACKAGE.zip
```

## Relatório final deve conter

```text
executive summary;
current state;
confirmed evidence;
unknowns;
root cause;
capability matrix;
false coverage risk;
contract/boundary analysis;
recommended architecture;
ADR draft summary;
implementation plan P0/P1/P2;
validation gates;
blockers;
owner decisions needed;
Devin next prompt.
```

---

## Quality gates por onda de sub-sessões

A sessão-mãe deve aplicar gates entre ondas:

### Gate W1 — Discovery Coverage Gate

```text
Só avançar para análise cruzada se SS-01 a SS-06 estiverem DONE ou se os BLOCKERS forem explícitos.
Deve existir mapa de paths cobertos/não cobertos.
Deve existir inventário inicial de parser antigo, motor BAL, DLM, gerador e constructs reais.
```

### Gate W2 — Cross-Shard Consistency Gate

```text
Só avançar para opções arquiteturais se parser antigo, motor BAL, DLM e gerador tiverem sido comparados.
Deve existir Construct Visibility Matrix.
Deve existir Dataflow/Producer/Consumer/Contract Map.
```

### Gate W3 — Implementation Quality Gate

```text
Só avançar para recomendação se a qualidade das camadas, builders, schemas, contracts e tests relevantes tiver sido auditada.
Deve existir smell register e refactor candidate matrix.
```

### Gate W4 — Pre-Decision Readiness Gate

```text
Só redigir ADR draft se PRE_DECISION_EVIDENCE_READINESS_CHECK.md for GO.
Se for NO-GO, produzir follow-up plan em vez de decisão final.
```

### Gate W5 — Red Team Gate

```text
Nenhuma recomendação final pode ser entregue sem SS_REDTEAM_RECOMMENDATION_CHALLENGE.md.
Findings do red team devem ser respondidos um a um.
```

## Requisito adicional em todas as fases

Em todas as fases, a sessão-mãe deve informar se a análise foi feita em sub-sessões reais ou workstreams simulados. Deve também atualizar:

```text
SUBSESSION_STATUS_BOARD.md
SUBSESSION_EVIDENCE_LEDGER.md
SUBSESSION_CONFLICT_LEDGER.md, quando houver conflitos
```

Nenhuma fase deve ser considerada completa se os achados das sub-sessões relevantes não tiverem sido integrados à síntese da sessão-mãe.

## Formato obrigatório de fechamento de cada fase

Ao final de cada fase, registrar no relatório da fase:

```text
## Fase executada
## Escopo
## Comandos executados
## Arquivos inspecionados
## Achados principais
## Decisões / hipóteses
## Producers / Consumers
## Artifacts / Contracts / Gates
## Findings
## Riscos
## Blockers
## Requirement → Evidence
## GO/NO-GO interno
## Decisão de continuidade
CONTINUE_AUTONOMOUSLY ou STOP_OWNER_INPUT_REQUIRED
## Próxima fase executada automaticamente, se aplicável
```

Não pedir comando para avançar quando a decisão for `CONTINUE_AUTONOMOUSLY`.

---

# Comando inicial para o Devin

Use esta mensagem:

```text
Modo: BAL Engine ↔ DLM ↔ Test Generator Architecture Investigation / No Implementation Yet.

Objetivo:
Investigar no repositório o gap arquitetural em que existe um motor BAL mais maduro/robusto, mas o gerador de testes ainda consome o parser BAL antigo/deficitário do DLM. A meta é descobrir o estado real, medir o risco de false coverage, auditar profundamente a qualidade das camadas, artifacts, schemas, contracts, specs, builders, boundaries e implementações atuais relacionadas à arquitetura-alvo V7, entender por que integrar o motor BAL ao DLM é difícil, comparar alternativas arquiteturais e recomendar a melhor solução para preparar o repo para a arquitetura-alvo ODM V7.

Inicie pela Fase 0 — Status de entrada e plano de investigação — e avance autonomamente pelas fases seguintes até concluir a Fase 8, salvo impeditivo grave.

Além disso, já na Fase 0, crie o plano de orquestração multi-sessão/sub-sessão com o máximo de paralelização analítica segura possível, priorizando qualidade, contexto ótimo, evidência e profundidade arquitetural.

Não implemente código.
Não altere o DLM.
Não substitua parser.
Não conecte motor BAL ao gerador.
Não crie quick fix.
Não assuma que a fala “é complexo” basta; explique a causa arquitetural com evidência.
Não declare cobertura robusta sem provar constructs suportados/visíveis.
Não trate o parser antigo como aceitável se ele omitir constructs silenciosamente.
Não viole a arquitetura-alvo ODM V7.

Use como referência:
- ODM_V7_DOCUMENTACAO_UNIFICADA_IMPLEMENTATION_PLAN_READY.md
- documentação-guia ODM V7 disponível no projeto/repo, se existir
- código real do repo, apenas como evidência do estado atual

Escopo obrigatório:
- analisar exclusivamente implementações relacionadas à arquitetura-alvo V7;
- não auditar a parte legada do repositório, salvo touchpoints que impactem diretamente o target V7;
- classificar cada path/módulo como TARGET_V7_CORE, TARGET_V7_SUPPORTING, TARGET_V7_ADAPTER, TARGET_V7_TEST, TARGET_V7_DEPENDS_ON_LEGACY, LEGACY_TOUCHPOINT_FOR_TARGET, LEGACY_OUT_OF_SCOPE ou UNKNOWN_NEEDS_CLASSIFICATION;
- gerar TARGET_V7_SCOPE_CLASSIFICATION.md, LEGACY_EXCLUSION_LEDGER.md e TARGET_LEGACY_TOUCHPOINT_RISK_REGISTER.md.

Ao final da Fase 0, entregue:
- repo/branch/status;
- fontes disponíveis;
- fontes ausentes;
- escopo e fora de escopo;
- hipóteses iniciais;
- estratégia de discovery;
- comandos planejados;
- riscos iniciais;
- GO/NO-GO para Fase 1;
- comando sugerido para avançar.
```
