# PROMPT DEVIN — Sessão 2 — P0.0 / N00 Repo Discovery ODM V7

## Modo da sessão

ODM Engineering Platform V7 — Sessão 2 — `P0.0 / N00 Repo Discovery`.

Esta sessão deve executar **exclusivamente** a etapa de Repo Discovery prevista na documentação-guia operacional Devin e no plano de implementação da nova arquitetura-alvo ODM V7.

Esta sessão **não** deve implementar código, refatorar, materializar contracts/schemas/builders/registries, alterar regras ODM, alterar comportamento funcional ou iniciar waves de implementação.

---

## 1. Pré-condições obrigatórias

Antes de iniciar, confirme se a Sessão 1 foi concluída com sucesso.

A Sessão 1 deve ter:

1. reconstruído e validado os 4 pacotes ODM V7;
2. instalado a nova documentação em:

```text
/docs/odm-v7-target-architecture/
```

3. preservado a documentação anterior como legado em:

```text
/docs/_legacy/
```

4. criado os entrypoints obrigatórios:

```text
/docs/odm-v7-target-architecture/README.md
/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md
/docs/odm-v7-target-architecture/DOCS_NAVIGATION_INDEX.md
/docs/odm-v7-target-architecture/SOURCE_AUTHORITY_FOR_DEVIN.md
```

5. atualizado referências do ecossistema do repo, incluindo quando aplicável:

```text
AGENTS.md
skills
knowledge sources
playbooks
prompts
manifests
índices internos
```

Se qualquer pré-condição não estiver satisfeita, **não execute discovery incompleto e não implemente nada**. Retorne:

```text
NO_GO_REQUIRES_DOCS_INSTALLATION_FIX
```

com a lista exata do que falta.

---

## 2. Objetivo da sessão

Executar o `P0.0 / N00 Repo Discovery` de forma segura, auditável e não destrutiva.

O objetivo é produzir um relatório real do repositório para orientar as waves/sessões/subsessões de implementação futuras.

Esta sessão deve descobrir e registrar:

- estrutura real do repositório;
- paths reais;
- módulos reais;
- packages reais;
- classes reais;
- scripts reais;
- comandos reais disponíveis;
- ferramentas reais de build/test/validation;
- boundaries reais;
- localização de assets IBM ODM/BRE, se existirem;
- localização de regras, XOM/BOM, exports, fixtures, tests, workbooks e docs existentes;
- gaps entre documentação e repo real;
- blockers reais;
- itens que precisam de Owner Review;
- DAG/waves/sessões recomendadas;
- primeira wave segura de implementação;
- Requirement→Evidence inicial.

---

## 3. Ponto inicial obrigatório

Comece por:

```text
/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md
```

Depois leia, nesta ordem:

```text
/docs/odm-v7-target-architecture/SOURCE_AUTHORITY_FOR_DEVIN.md
/docs/odm-v7-target-architecture/DOCS_NAVIGATION_INDEX.md
/docs/odm-v7-target-architecture/30_devin_operational_guide/
/docs/odm-v7-target-architecture/40_implementation_plan/
/docs/odm-v7-target-architecture/20_chatgpt_optimized_support_pack/
/docs/odm-v7-target-architecture/10_canonical_odm_documentation/
```

Use o menor contexto suficiente. Não tente ler a documentação inteira por padrão.

---

## 4. Hierarquia documental obrigatória

Aplique a seguinte autoridade:

1. Decision Ledger ou ADR aprovado mais recente, se existir.
2. Documentação canônica ODM V7 em:

```text
/docs/odm-v7-target-architecture/10_canonical_odm_documentation/
```

3. Contracts/specs/architecture da documentação canônica.
4. IBM ODM docs/evidências reais, quando houver claim IBM-specific.
5. Support pack otimizado em:

```text
/docs/odm-v7-target-architecture/20_chatgpt_optimized_support_pack/
```

apenas como roteamento/localização, não como fonte primária em conflito.

6. Documentação-guia operacional Devin em:

```text
/docs/odm-v7-target-architecture/30_devin_operational_guide/
```

como instrução de operação.

7. Plano de implementação em:

```text
/docs/odm-v7-target-architecture/40_implementation_plan/
```

como plano de execução.

8. Repo discovery real como autoridade para claims sobre paths, comandos, módulos, classes, packages, scripts, estrutura física e estado observável do repositório.

---

## 5. Invariantes obrigatórios

Preserve os invariantes abaixo:

- O Canonical ODM Model é a fonte única editável corrente das regras.
- Artefatos derivados não são fonte primária de mudança.
- IBM ODM Real permanece referência comportamental externa e observável.
- IBM ODM Documentation governa claims IBM-specific.
- Output igual não prova equivalência comportamental plena.
- Simulador é engine operacional interna dentro do support scope declarado.
- Candidate expected output não vira verified expected output sem Promotion Gate.
- Workbook é artifact terminal de uso humano, não fonte de regra, knowledge, export, publish ou Devin Index content.
- Devin Index / Context Lookup indexam conhecimento conhecido e evidências observáveis; não inferem internals inacessíveis do IBM ODM Real.
- Prompts, playbooks, índices, summaries e relatórios são derivados.
- Claims de repo exigem repo discovery.
- Claims IBM ODM/BRE exigem IBM docs, SME/Owner review, execução real, relatório, teste ou blocker explícito.
- ADR drafts continuam `DRAFT / NEEDS_REVIEW / NO_ADR_APPROVAL`, salvo se um ADR aprovado for fornecido explicitamente.
- Lacunas devem ser marcadas como `PENDENTE`, `NEEDS_REVIEW`, `NEEDS_ADR`, `NEEDS_REPO_DISCOVERY`, `NEEDS_IBM_DOCS`, `NEEDS_REAL_ODM_VALIDATION` ou `BLOCKER`.

---

## 6. Escopo real do projeto

O projeto opera em repositório de testes, restrito ao time.

Não há obrigação de:

- pipeline CI/CD obrigatório;
- deployment produtivo;
- promoção para produção;
- release governance produtiva;
- SLO/SLI/SLA/RTO/RPO;
- observabilidade produtiva;
- nova política formal de secrets;
- RBAC produtivo por ambiente;
- SBOM/signing/provenance produtivo.

A ausência desses itens **não deve ser tratada como blocker atual**.

Se algo disso existir no repo, registre como evidência observada, mas não trate como requisito obrigatório salvo se a documentação/Owner determinar explicitamente.

---

## 7. Regras de segurança e anti-alucinação

Durante o discovery:

- Não invente paths, comandos, packages, módulos, classes, owners técnicos, scripts ou baselines.
- Toda afirmação sobre o repo deve ter evidência observável.
- Se algo não for encontrado, use `NOT_FOUND`, `PARTIAL`, `NEEDS_REPO_DISCOVERY_FOLLOWUP` ou `BLOCKER`.
- Não declare production readiness.
- Não declare CI validated.
- Não declare deployment readiness.
- Não declare importability verified.
- Não declare publish ready.
- Não declare full behavioral equivalence.
- Não invente comportamento IBM ODM/BRE.
- Não aprove ADRs.
- Não altere regras ODM.
- Não faça mudanças de código.
- Não faça refatoração.
- Não materialize contracts/schemas/builders/registries nesta sessão.

---

## 8. Comandos permitidos nesta sessão

A sessão deve ser segura e não destrutiva.

Pode usar comandos de inspeção, por exemplo:

```text
pwd
ls
find
tree
rg
grep
cat
sed -n
head
tail
git status
git branch
git log --oneline -n <N>
```

Pode ler arquivos de build/configuração, por exemplo:

```text
pom.xml
build.gradle
settings.gradle
package.json
Makefile
Dockerfile
README.md
AGENTS.md
```

Pode identificar comandos de build/test/validation.

Se decidir executar algum comando de build/test para caracterização inicial, só faça se for seguro e não destrutivo. Registre:

- comando;
- path;
- motivo;
- resultado;
- limitação;
- impacto no discovery.

Não execute comandos destrutivos, deploy, publish, import/export real ou scripts que alterem ambientes sem Owner Review.

---

## 9. Escopo detalhado de discovery

Faça uma varredura orientada por evidência incluindo, quando aplicável:

### 9.1 Estrutura do repo

- raiz do repo;
- branch atual;
- arquivos raiz relevantes;
- módulos/submódulos;
- estrutura de pastas;
- docs existentes;
- documentação legada ODM V7;
- documentação nova instalada.

### 9.2 Ecossistema operacional Devin/repo

Verifique referências e entrypoints como:

```text
AGENTS.md
skills
knowledge sources
playbooks
prompts
manifests
context indexes
DevIn/Devin files
scripts de automação
```

### 9.3 Código e arquitetura real

Mapeie apenas o que existir:

- packages;
- classes;
- services;
- adapters;
- ports;
- validators;
- builders;
- registries;
- schemas;
- simulador;
- harness;
- export/publish;
- migration utilities;
- tests;
- fixtures.

### 9.4 IBM ODM / BRE assets

Mapeie, se existirem:

- exports;
- XOM/BOM;
- rules;
- decision services;
- ruleflows;
- workbooks;
- expected outputs;
- fixtures;
- traces observáveis;
- IBM docs locais;
- scripts de import/export/test;
- relatórios anteriores.

Não declare importability, publish readiness ou equivalência. Apenas registre evidências observadas.

### 9.5 Build/test/validation

Identifique:

- comandos reais disponíveis;
- scripts;
- testes unitários/integrados;
- linters;
- validators;
- harness;
- fixtures;
- comandos de geração/validação;
- limitações;
- blockers.

---

## 10. Saída obrigatória

Produza exatamente o relatório:

```text
P0_0_N00_REPO_DISCOVERY_REPORT
```

A resposta deve ter a estrutura abaixo.

---

# P0_0_N00_REPO_DISCOVERY_REPORT

## 1. Status de entrada

Inclua:

- repo analisado;
- branch atual;
- status git inicial;
- documentação ODM V7 nova encontrada;
- entrypoints encontrados;
- documentação legada encontrada;
- pré-condições confirmadas;
- GO/NO-GO de entrada.

## 2. Fontes documentais consultadas

Inclua:

- arquivos consultados;
- por que foram consultados;
- hierarquia documental aplicada;
- documentos ainda não consultados e por quê.

## 3. Estrutura real do repositório

Inclua:

- árvore resumida;
- módulos principais;
- diretórios relevantes;
- arquivos raiz relevantes;
- observações.

## 4. Mapa documentação → repo real

Monte tabela:

| Área ODM V7 | Documento de referência | Path real observado | Status | Evidência | Gap/observação |
|---|---|---|---|---|---|

Status permitidos:

```text
FOUND
PARTIAL
NOT_FOUND
NEEDS_IMPLEMENTATION
NEEDS_OWNER_REVIEW
BLOCKER
```

## 5. Módulos/packages/classes/scripts reais

Liste apenas itens observados.

Para cada item:

- tipo;
- path;
- nome;
- evidência;
- relação provável com ODM V7;
- confiança: `HIGH`, `MEDIUM`, `LOW`.

Não inferir além da evidência.

## 6. Comandos reais disponíveis

Monte tabela:

| Comando | Path | Finalidade | Evidência | Status | Observação |
|---|---|---|---|---|---|

Status permitidos:

```text
AVAILABLE
NOT_AVAILABLE
BLOCKED
NEEDS_VALIDATION
EXECUTED_PASS
EXECUTED_FAIL
```

## 7. IBM ODM / Real ODM assets

Inclua:

- assets encontrados;
- paths;
- tipo;
- evidência;
- limitações;
- claims que permanecem bloqueados;
- itens que exigem IBM Docs;
- itens que exigem Real ODM validation;
- itens que exigem Owner Review.

## 8. Gaps reais

Classifique cada gap:

| Gap | Evidência | Classificação | Impacto | Próxima ação |
|---|---|---|---|---|

Classificações:

```text
NEEDS_IMPLEMENTATION
NEEDS_REPO_DISCOVERY_FOLLOWUP
NEEDS_IBM_DOCS
NEEDS_REAL_ODM_VALIDATION
NEEDS_OWNER_REVIEW
BLOCKER
OUT_OF_SCOPE_BY_OWNER_DECISION
```

## 9. Blockers reais

Separe:

### 9.1 Blockers reais

Itens que impedem iniciar implementação.

### 9.2 Não-blockers por decisão Owner

Itens como ausência de CI/CD obrigatório, produção, deployment, SLO/RTO/RPO, observabilidade produtiva ou nova política formal de secrets.

## 10. DAG / waves / sessões recomendadas

Proponha a sequência real de implementação pós-discovery.

Para cada wave/sessão:

| Wave/Sessão | Objetivo | Paths envolvidos | Docs a consultar | Entrada | Saída esperada | Gates | Validação | Blockers |
|---|---|---|---|---|---|---|---|---|

## 11. Primeira wave segura recomendada

Inclua:

- nome da wave;
- objetivo;
- por que é segura;
- paths;
- docs;
- gates;
- validação;
- riscos;
- prompt sugerido para a próxima sessão de implementação.

## 12. Requirement → Evidence inicial

Monte tabela:

| Requirement | Evidence | Status | Gap/Blocker |
|---|---|---|---|

## 13. Owner Review necessário

Liste perguntas ao Owner apenas se forem necessárias.

Para cada pergunta:

- pergunta;
- contexto;
- impacto;
- decisão necessária;
- consequência se não respondida.

## 14. Riscos

Liste riscos técnicos, documentais e operacionais.

## 15. Veredito final

Declare exatamente um:

```text
GO_FOR_FIRST_IMPLEMENTATION_WAVE
PARTIAL_GO_WITH_WARNINGS
NO_GO_REQUIRES_OWNER_REVIEW
NO_GO_REQUIRES_REPO_DISCOVERY_FIX
NO_GO_BLOCKED
```

Não implemente nada nesta sessão.

---

## 11. Critério de sucesso da sessão

A sessão só passa se:

- não implementou código;
- não alterou regras ODM;
- não inventou paths/comandos/classes/packages;
- consultou os entrypoints obrigatórios;
- produziu mapa documentação → repo real;
- identificou comandos reais;
- identificou gaps reais;
- separou blockers reais de itens fora de escopo;
- preservou IBM/Real ODM gates;
- propôs DAG/waves/sessões;
- indicou a primeira wave segura ou declarou NO-GO;
- produziu Requirement→Evidence inicial.

---

## 12. Próxima sessão

Se o veredito final for:

```text
GO_FOR_FIRST_IMPLEMENTATION_WAVE
```

ou:

```text
PARTIAL_GO_WITH_WARNINGS
```

e o Owner aceitar os warnings, então a próxima sessão deve iniciar a primeira wave de implementação usando o prompt operacional de implementação guiada pela documentação ODM V7.

A próxima sessão deve nascer do relatório desta Sessão 2, não de suposições anteriores.

