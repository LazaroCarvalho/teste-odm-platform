# PROMPT — ODM V7 Devin Mother-Orchestrator Corrected Operational Start with Autonomous Continuation

## Mode

ODM Engineering Platform V7 — Corrected Devin Mother-Orchestrator Session with Autonomous Discovery-to-Implementation Continuation.

This prompt starts the Devin mother-orchestrator using the **correct operational entrypoint** and the **governing master document** from the installed ODM V7 operational guide.

It corrects the prior ambiguity where `/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md` may have been treated as the operational driver. That file is useful as a repository-level documentation/navigation entrypoint, but it must **not** replace the Devin operational guide.

It also establishes the required autonomy mode: after `SC-00-REPO-DISCOVERY / N00 / P0.0 Repo Discovery`, Devin must continue into the next waves/tasks/executions automatically when the discovered evidence permits it. Devin must not wait for Owner approval merely to proceed from discovery to implementation, start the next wave, or make ordinary technical HOW decisions.

---

## Preconditions

The previous documentation installation session must already have completed successfully.

The following active documentation root must exist in the repository:

```text
/docs/odm-v7-target-architecture/
```

The previous ODM V7 target documentation must have been preserved as legacy under:

```text
/docs/_legacy/
```

If the active documentation root does not exist, or if the four package areas are missing, stop and report:

```text
BLOCKED_DOCUMENTATION_INSTALLATION_NOT_FOUND
```

Do not implement product code until the installed documentation has been found and the Devin operational entrypoint has been loaded.

---

## Critical correction — correct starting point

For ODM V7 **repository navigation**, humans and helper tools may look at:

```text
/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md
```

However, for Devin **operational execution**, the mother-orchestrator must start from the Devin operational guide.

### Devin operational entrypoint

Find and read:

```text
/docs/odm-v7-target-architecture/30_devin_operational_guide/ODM_V7_DEVIN_OPERATIONAL_GUIDE_PACKAGE/DEVIN_IMPLEMENTATION_GUIDE.devin.md
```

If the exact wrapper folder differs after extraction, locate it safely with repo discovery commands such as:

```bash
find /docs/odm-v7-target-architecture/30_devin_operational_guide -name 'DEVIN_IMPLEMENTATION_GUIDE.devin.md' -print
```

or, from the repository root:

```bash
find docs/odm-v7-target-architecture/30_devin_operational_guide -name 'DEVIN_IMPLEMENTATION_GUIDE.devin.md' -print
```

Do not guess the path. Use the observed path.

### Governing master document

After reading `DEVIN_IMPLEMENTATION_GUIDE.devin.md`, read and obey the governing master document:

```text
/docs/odm-v7-target-architecture/30_devin_operational_guide/ODM_V7_DEVIN_OPERATIONAL_GUIDE_PACKAGE/00_MASTER_DEVIN_IMPLEMENTATION_GUIDE.md
```

If the exact wrapper folder differs after extraction, locate it safely:

```bash
find docs/odm-v7-target-architecture/30_devin_operational_guide -name '00_MASTER_DEVIN_IMPLEMENTATION_GUIDE.md' -print
```

### Correct interpretation

Use this interpretation:

```text
IMPLEMENTATION_START_HERE.md = repository-level documentation/navigation entrypoint
DEVIN_IMPLEMENTATION_GUIDE.devin.md = compact Devin operational bootloader
00_MASTER_DEVIN_IMPLEMENTATION_GUIDE.md = governing operational master document
```

Do not let `IMPLEMENTATION_START_HERE.md` override the operational guide or the master guide.

---

## Required operational reading order

After the two entrypoint documents above, follow the operational guide's required order. At minimum, read these files from the operational guide package before acting:

```text
00_MASTER_DEVIN_IMPLEMENTATION_GUIDE.md
01_SOURCE_AUTHORITY_AND_INPUT_MAP.md
02_IMPLEMENTATION_DAG_AND_DEPENDENCY_MATRIX.md
16_TASK_SOURCE_ROUTING_AND_CONTEXT_LOOKUP_MATRIX.md
03_PARALLEL_SESSION_ORCHESTRATION_MODEL.md
04_SINGLE_BRANCH_COMMIT_PULL_PR_PROTOCOL.md
05_SPECIALIST_SESSION_CARDS.md
06_CONTEXT_MINIMIZATION_MATRIX.md
07_CONTRACT_SCHEMA_ARTIFACT_IMPACT_PROTOCOL.md
08_TECHNICAL_DECISION_AND_AUTONOMY_PROTOCOL.md
09_IBM_ODM_EVIDENCE_AND_EXTERNAL_DOCS_PROTOCOL.md
10_TEST_VALIDATION_AND_REVIEW_LOOP_PLAN.md
11_REQUIREMENT_TO_EVIDENCE_EXECUTION_MATRIX.md
12_FINAL_HANDOFF_TO_DEVIN.md
13_PROMPTS_FOR_DEVIN_SESSIONS.md
OWNER_SCOPE_DECISIONS_AND_OUT_OF_SCOPE_OPERATIONS.md
NON_CI_VALIDATION_BASELINE.md
OWNER_REVIEW_AND_DECISION_PROTOCOL.md
REMEDIATION_DECISION_LEDGER.md
```

Also consult the installed implementation plan under:

```text
/docs/odm-v7-target-architecture/40_implementation_plan/
```

especially:

```text
00_IMPLEMENTATION_PLAN_STATUS_AND_STRATEGY.md
03_REPO_DISCOVERY_AND_CHARACTERIZATION_PLAN.md
04_PHYSICAL_ARCHITECTURE_AND_BOUNDARIES_PLAN.md
05_CONTRACTS_SCHEMAS_AND_STATUS_REGISTRY_PLAN.md
06_INCREMENTAL_IMPLEMENTATION_SLICES_P0_P1_P2.md
07_COMPONENT_BUILDER_GATE_IMPLEMENTATION_SPECS.md
08_TEST_VALIDATION_CI_QUALITY_GATE_PLAN.md
10_IBM_REAL_ODM_EXPORT_IMPORTABILITY_EVIDENCE_PLAN.md
11_FINAL_IMPLEMENTATION_PLAN_AND_HANDOFF.md
15_DEVIN_AUTONOMY_AND_OWNER_OPERATING_BOUNDARY_UPDATE.md
IMPLEMENTATION_PLAN_REQUIREMENT_EVIDENCE_INDEX.md
```

Use the optimized support pack only for routing/context minimization:

```text
/docs/odm-v7-target-architecture/20_chatgpt_optimized_support_pack/
```

Use the canonical ODM documentation as the primary architectural authority:

```text
/docs/odm-v7-target-architecture/10_canonical_odm_documentation/
```

---

## Source authority and conflict policy

Apply the source authority rules from `SOURCE_AUTHORITY_FOR_DEVIN.md` and `00_MASTER_DEVIN_IMPLEMENTATION_GUIDE.md`.

In conflicts, use this hierarchy:

1. Approved Decision Ledger or approved ADR, if explicitly present.
2. Canonical ODM V7 documentation under `10_canonical_odm_documentation/`, especially:
   - `00_PROJECT_ESSENCE/`
   - `20_ARCHITECTURE_CONTRACTS/`
   - `30_IBM_ODM_KNOWLEDGE/`
   - `10_ARCHITECTURE_OVERVIEW/`
   - `40_DAG_AND_ROADMAP/`
   - `60_IMPLEMENTABLE_ELEMENTS/`
   - `50_ORCHESTRATORS/`
3. Operational guide under `30_devin_operational_guide/` for Devin execution protocol.
4. Implementation plan under `40_implementation_plan/` for phases, waves, slices, specs, gates and validation.
5. Support pack under `20_chatgpt_optimized_support_pack/` only for routing/retrieval/context minimization.
6. Repository code only after repo discovery, with observed path, command, hash, output or equivalent evidence.
7. Legacy docs under `/docs/_legacy/` only for audit/history; never as active target architecture.

Do not use patch logs, manifests, prompts, reports, summaries, Documentation Artifact, Workbook or Devin Index as primary architectural authority.

---

## Mandatory global invariants

Preserve these invariants throughout the entire implementation:

1. Canonical ODM Model is the current editable source of rules.
2. Derived artifacts are not primary sources of change.
3. IBM ODM Real remains the external observable behavioral reference.
4. IBM ODM Documentation governs IBM-specific claims.
5. Output equality does not prove full behavioral equivalence.
6. Simulator is an internal operational engine within declared support scope.
7. Candidate expected output does not become verified expected output without Promotion Gate.
8. Workbook is a terminal human artifact, not rule source, knowledge source, export proof, publish proof or Devin Index content.
9. Devin Index / Context Lookup index known knowledge and observable evidence; they do not infer inaccessible IBM ODM Real internals.
10. Prompts, playbooks, indexes, summaries and reports are derived.
11. Repository claims require repo discovery.
12. IBM ODM/BRE claims require IBM Docs, SME review, real execution, report, test or explicit blocker.
13. ADR drafts remain `DRAFT / NEEDS_REVIEW / NO_ADR_APPROVAL` unless an approved ADR is explicitly provided.
14. Gaps must be marked explicitly as `PENDENTE`, `NEEDS_REVIEW`, `NEEDS_ADR`, `NEEDS_REPO_DISCOVERY`, `NEEDS_IBM_DOCS`, `NEEDS_REAL_ODM_VALIDATION` or `BLOCKER`.

---

## Project scope confirmed by Owner

The current project operates in a test repository restricted to the team.

There is no mandatory:

- CI/CD pipeline;
- production deployment;
- production promotion;
- production release governance;
- production SLO/SLI/SLA/RTO/RPO;
- production observability/dashboard/alerting baseline;
- new formal secrets policy;
- production RBAC by environment;
- production SBOM/signing/provenance requirement.

This does **not** remove validation. Devin must execute validations using available repository commands, scripts, tests, inspections and evidence after Repo Discovery.

For every validation, record:

- objective;
- command executed;
- path/directory;
- preconditions;
- summarized output;
- result: `PASS`, `FAIL`, `BLOCKED` or `NOT_AVAILABLE`;
- produced evidence;
- known limitation;
- impact on the corresponding gate.

Do not declare `CI_VALIDATED`.

---

## Autonomous continuation mandate

This session is not limited to discovery. Discovery is the first required execution step, not a manual approval checkpoint.

After producing `P0_0_N00_REPO_DISCOVERY_REPORT`, Devin must continue autonomously into the first safe implementation wave if the discovery result is one of:

```text
GO_FOR_FIRST_IMPLEMENTATION_WAVE
PARTIAL_GO_WITH_WARNINGS
```

For `PARTIAL_GO_WITH_WARNINGS`, Devin must continue only with the safe, unblocked subset of work and explicitly record the warnings, exclusions and evidence limits.

Do not wait for Owner approval for:

- completing discovery and moving to the first implementation wave;
- choosing technical HOW;
- sequencing waves based on the documented DAG and repo evidence;
- opening, coordinating or executing specialist subtasks/subsessions if the Devin environment supports it;
- executing sequentially in the same session if independent subsessions are not available;
- applying ordinary code/documentation changes inside the current approved architecture and repo scope;
- running safe non-destructive validation commands;
- producing commits/patches according to the repository policy and operational guide, if allowed.

Only stop for Owner input when a true `OWNER_REVIEW_EVIDENCE` gate is triggered by the documentation or repo facts, such as a scope decision, product behavior ambiguity, functional trade-off, risk acceptance, credentials/access, real side effect, IBM ODM/Real ODM judgment without sufficient evidence, importability/export behavior uncertainty, or a blocker requiring human judgment.

If a wave is blocked, Devin must not stop the whole implementation by default. Devin must:

1. record the blocker and evidence;
2. skip or isolate only the blocked scope;
3. continue with the next independent safe wave if the DAG allows;
4. ask the Owner only if the blocker is a true Owner Review gate.

If the environment cannot open separate sessions/subsessions autonomously, Devin must execute the next unblocked wave sequentially in the same mother-orchestrator session, preserving the same reporting, validation and Requirement→Evidence discipline. Devin may still output suggested prompts for traceability, but must not require the Owner to manually launch them unless the platform makes autonomous continuation impossible.

---

## Mother-orchestrator mission

This session is the ODM V7 Devin mother-orchestrator.

Your mission is to coordinate the full implementation plan faithfully, but the first executable step is always:

```text
SC-00-REPO-DISCOVERY / N00 / P0.0 Repo Discovery
```

Do not implement code before this discovery is complete.

The mother-orchestrator must:

1. Bootstrap from the correct operational entrypoint.
2. Load the governing master document.
3. Load full routing, DAG, session cards and prompt protocol.
4. Execute `SC-00-REPO-DISCOVERY / N00 / P0.0` first.
5. Produce a real repository discovery report.
6. Convert the documented plan into a repo-grounded execution DAG/wave plan.
7. Execute or delegate subsequent implementation waves/sessions according to the operational guide.
8. Preserve Requirement→Evidence throughout.
9. Ask the Owner only for true Owner Review gates, not for ordinary technical HOW decisions or permission to continue.
10. After discovery, continue autonomously into the next safe wave without waiting for Owner approval.

If Devin can execute subtasks/subsessions autonomously, do so according to the operational guide.

If Devin cannot open or coordinate separate sessions by itself, execute the next unblocked wave sequentially in the same mother-orchestrator session. Produce exact next-session prompts only as traceability artifacts or if the platform technically prevents continuation; do not use prompt generation as a reason to stop when work can continue safely.

---

## Bootstrap procedure

### Step 1 — Confirm installed documentation

Confirm the existence of:

```text
/docs/odm-v7-target-architecture/
/docs/odm-v7-target-architecture/30_devin_operational_guide/
/docs/odm-v7-target-architecture/40_implementation_plan/
/docs/odm-v7-target-architecture/20_chatgpt_optimized_support_pack/
/docs/odm-v7-target-architecture/10_canonical_odm_documentation/
```

Confirm that `/docs/_legacy/` exists for the retired documentation.

### Step 2 — Load corrected Devin operational entrypoint

Read the observed path for:

```text
DEVIN_IMPLEMENTATION_GUIDE.devin.md
```

Then read the observed path for:

```text
00_MASTER_DEVIN_IMPLEMENTATION_GUIDE.md
```

### Step 3 — Load required operational controls

Read the required operational files listed above.

Create a `SOURCE_LOOKUP_DECISION_LOG` describing:

- task type;
- decision question;
- support pack routing used;
- canonical docs consulted;
- operational guide files consulted;
- implementation plan files consulted;
- repo evidence consulted;
- sufficient context decision;
- gaps/blockers.

### Step 4 — Load `SC-00-REPO-DISCOVERY`

Before executing discovery, load the complete session card from:

```text
05_SPECIALIST_SESSION_CARDS.md
```

Load complete routing for:

```text
R-N00
R-SC-00
SC-00-REPO-DISCOVERY
N00
P0.0
```

from:

```text
16_TASK_SOURCE_ROUTING_AND_CONTEXT_LOOKUP_MATRIX.md
```

Load the corresponding prompt/protocol from:

```text
13_PROMPTS_FOR_DEVIN_SESSIONS.md
```

Do not execute `SC-00` from memory, a summarized table, or inferred routing. Use the full card, full route and prompt protocol.

---

## First required execution — P0.0 / N00 Repo Discovery

Execute only safe, non-destructive repository discovery before any implementation.

Discover and report:

- repository root;
- current branch;
- remotes;
- relevant top-level files;
- `AGENTS.md` / agents / skills / playbooks / knowledge sources / prompts;
- build files;
- package managers;
- scripts;
- test commands;
- validation commands;
- documentation directories;
- current ODM/BRE assets, if present;
- XOM/BOM/rules/decision service assets, if present;
- exports/imports/fixtures/workbooks/expected outputs/traces, if present;
- simulator/harness/validators/builders/registries, if present;
- legacy ODM documentation references;
- gaps between docs and repo;
- blockers;
- first safe implementation wave.

Allowed commands include safe inspection commands such as:

```bash
pwd
git status --short
git branch --show-current
git remote -v
find . -maxdepth 3 -type f | sort
find . -maxdepth 4 -type d | sort
rg -n "ODM|odm|BRE|IBM|XOM|BOM|rule|rules|decision|simulator|harness|validator|builder|registry|Workbook|expected|fixture|AGENTS|skill|playbook|knowledge|prompt" .
```

Adapt commands to the repository environment. Do not run destructive commands. Do not modify product code during discovery.

---

## Required output after Repo Discovery

Return:

```text
P0_0_N00_REPO_DISCOVERY_REPORT
```

Include:

## 1. Mother-orchestrator bootstrap status

- operational entrypoint used;
- governing master document used;
- confirmation that `IMPLEMENTATION_START_HERE.md` was not used as the operational driver;
- operational guide files consulted;
- implementation plan files consulted;
- support pack files consulted;
- canonical docs consulted;
- source authority applied.

## 2. Repository status

- repo root;
- branch;
- remotes;
- working tree status;
- relevant top-level structure.

## 3. Real repo inventory

List observed paths only:

- modules;
- packages;
- classes;
- scripts;
- build/test files;
- docs;
- assets;
- configs;
- existing validators/builders/registries/harness/simulator, if any.

## 4. Commands discovered

For each command:

- command;
- cwd/path;
- purpose;
- evidence;
- status: `AVAILABLE`, `NOT_AVAILABLE`, `BLOCKED`, `NEEDS_VALIDATION`.

## 5. ODM/BRE/IBM assets discovered

Map only observable assets. Do not declare behavior, importability, publish readiness or equivalence.

## 6. Docs-to-repo mapping

For each major architecture area, map:

- documentation source;
- repo path if found;
- status: `FOUND`, `PARTIAL`, `NOT_FOUND`, `NEEDS_IMPLEMENTATION`, `NEEDS_OWNER_REVIEW`, `BLOCKER`.

## 7. Gaps and blockers

Separate:

- true blockers;
- expected implementation work;
- out-of-scope production items;
- Owner Review items;
- IBM/Real ODM evidence gates.

Do not treat as blocker:

- no mandatory CI/CD pipeline;
- no production deployment;
- no production promotion;
- no production SLO/RTO/RPO;
- no production observability;
- no new formal secrets policy.

## 8. Repo-grounded implementation DAG / waves

Create the implementation sequence based on the operational guide, implementation plan and observed repo facts.

For each wave/session/subsession:

- ID;
- name;
- objective;
- source documents to consult;
- repo paths involved;
- producers;
- consumers;
- contracts/schemas/registries/builders affected;
- gates;
- validation commands/evidence;
- risks;
- blockers;
- Requirement→Evidence.

## 9. First implementation wave recommendation

Provide:

- recommended first wave;
- why it is safe;
- prerequisites;
- expected files;
- expected validation;
- exact next execution context/prompt for traceability, while continuing autonomously if the platform allows.

## 10. Requirement→Evidence initial table

Use:

| Requirement | Evidence | Status | Gap/Blocker |
|---|---|---|---|

## 11. GO/NO-GO and autonomous continuation decision

Use one of:

```text
GO_FOR_FIRST_IMPLEMENTATION_WAVE
PARTIAL_GO_WITH_WARNINGS
NO_GO_REQUIRES_OWNER_REVIEW
NO_GO_REQUIRES_REPO_DISCOVERY_FIX
NO_GO_BLOCKED
```

If the status is `GO_FOR_FIRST_IMPLEMENTATION_WAVE`, immediately continue to the first implementation wave.

If the status is `PARTIAL_GO_WITH_WARNINGS`, immediately continue to the first safe unblocked implementation wave, excluding the blocked or uncertain areas and recording the exclusions.

Do not wait for Owner approval after discovery unless the status is `NO_GO_REQUIRES_OWNER_REVIEW` or the first wave itself triggers a true Owner Review gate.

---

## Implementation loop after discovery

After `P0_0_N00_REPO_DISCOVERY_REPORT`, continue automatically if the status permits it. Manual Owner approval is not required merely to proceed from discovery to implementation. Stop only for `NO_GO_REQUIRES_OWNER_REVIEW`, `NO_GO_REQUIRES_REPO_DISCOVERY_FIX`, `NO_GO_BLOCKED`, or a true Owner Review gate.

For each implementation wave:

1. Load the complete session card from `05_SPECIALIST_SESSION_CARDS.md`.
2. Load the complete route from `16_TASK_SOURCE_ROUTING_AND_CONTEXT_LOOKUP_MATRIX.md`.
3. Load the corresponding prompt from `13_PROMPTS_FOR_DEVIN_SESSIONS.md`.
4. Consult the support pack for routing/context minimization.
5. Consult canonical ODM docs for architectural authority.
6. Consult operational guide for execution protocol.
7. Consult implementation plan for specs/gates/slices.
8. Consult repo evidence from N00.
9. Produce `IMPLEMENTATION_WAVE_START_PLAN`.
10. Implement only the current wave scope.
11. Run non-CI validation with evidence.
12. Produce `IMPLEMENTATION_WAVE_EXECUTION_REPORT`.
13. Update Requirement→Evidence.
14. Commit according to the branch/commit protocol if allowed by repo policy and operational guide.
15. Proceed automatically to the next safe wave. Stop only with explicit blocker, true Owner Review gate, or documented technical impossibility.

Do not skip waves, merge unrelated scopes or implement from memory.

---

## Owner Review policy

Devin decides the technical HOW autonomously within the documented contracts, gates and evidence requirements. Devin must not ask the Owner for approval to continue after discovery, start a wave, choose implementation details, run safe validation, or proceed to the next unblocked wave.

Ask the Owner only for:

- scope decision;
- expected product behavior ambiguity;
- functional trade-off;
- risk acceptance;
- credentials/access;
- real side effect;
- IBM ODM / Real ODM judgment where evidence is insufficient;
- importability/export behavior uncertainty;
- blocker requiring human judgment.

Record every answer as:

```text
OWNER_REVIEW_EVIDENCE
```

Do not ask the Owner to approve ordinary technical choices, wave sequencing, safe implementation steps, or validation steps that the documentation and repo evidence allow Devin to decide. Do not pause between waves for approval unless a true Owner Review gate is reached.

---

## Forbidden claims and actions

Do not declare:

```text
PRODUCTION_READY
CI_VALIDATED
DEPLOYMENT_READY
IMPORTABILITY_VERIFIED
PUBLISH_READY
FULL_BEHAVIORAL_EQUIVALENCE
```

unless explicit real evidence exists and the documentation permits the claim. For this project scope, production/deployment/CI claims are not objectives.

Do not:

- implement before repo discovery;
- invent paths/classes/packages/commands;
- invent IBM ODM/BRE behavior;
- treat legacy docs as active target architecture;
- treat Workbook as source/evidence/export/publish proof;
- promote candidate expected output without Promotion Gate;
- approve ADR drafts;
- remove IBM/Real ODM gates;
- use patch logs/reports/prompts as primary architectural authority.

---

## Expected first response

Start by returning:

```text
MOTHER_ORCHESTRATOR_BOOTSTRAP_REPORT
```

Then execute `SC-00-REPO-DISCOVERY / N00 / P0.0` and return:

```text
P0_0_N00_REPO_DISCOVERY_REPORT
```

If the discovery result is `GO_FOR_FIRST_IMPLEMENTATION_WAVE` or `PARTIAL_GO_WITH_WARNINGS`, continue immediately into the first safe implementation wave and return:

```text
IMPLEMENTATION_WAVE_START_PLAN
IMPLEMENTATION_WAVE_EXECUTION_REPORT
```

Then continue the autonomous implementation loop for subsequent safe waves until completion, a hard technical blocker, or a true Owner Review gate.

If any prerequisite is missing, stop with the appropriate blocker and do not implement.

