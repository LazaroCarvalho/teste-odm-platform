# PROMPT — Devin Reconstruction and Installation of Four ODM V7 Documentation Packages

## Mode

ODM Engineering Platform V7 — Four-Package Documentation Reconstruction, Repository Installation, Legacy Retirement, Navigation Entrypoint Creation, and Reference Migration.

## Inputs expected

Attach or provide the Markdown container:

`ODM_V7_FOUR_PACKAGES_UNIFIED_CONTAINER_FOR_DEVIN.md`

This container includes four ZIP payloads encoded in base64, package-level SHA-256 hashes, and per-file audit payloads.

## Goal

Reconstruct the four source ZIP packages byte-for-byte from the Markdown container, validate integrity, install the new documentation under `/docs`, retire the previous ODM V7 target documentation as legacy, create canonical navigation entrypoints for future Devin work, and update repository references that point to the superseded documentation.

## Packages to reconstruct

| Package ID | Canonical ZIP filename | Role |
|---|---|---|
| `P01_CANONICAL_ODM_DOCUMENTATION` | `ZIP_FULL_POS_CLEANUP.zip` | Primary updated ODM V7 documentation / authoritative architecture guide |
| `P02_CHATGPT_OPTIMIZED_SUPPORT_PACK` | `ODM_CHATGPT_OPTIMIZED_SUPPORT_PACK.zip` | Derived support pack for routing/retrieval |
| `P03_DEVIN_OPERATIONAL_GUIDE` | `ODM_V7_DEVIN_OPERATIONAL_GUIDE_PACKAGE_REMEDIATED_FINAL_DEVIN_HANDOFF_CLEAN.zip` | Operational guide for Devin |
| `P04_IMPLEMENTATION_PLAN` | `ODM_V7_IMPLEMENTATION_PLAN_FINAL_DEVIN_AUTONOMY_UPDATE_REMEDIATED_FINAL_DEVIN_HANDOFF_CLEAN.zip` | Final implementation plan |

## Absolute rules

- Do not edit the Markdown container by hand.
- Do not reconstruct ZIPs from copied prose.
- The `ZIP_BASE64` blocks are the authoritative source for exact ZIP reconstruction.
- Internal `FILE_BASE64` blocks are audit payloads and must be used to validate extracted file contents.
- Do not delete the previous repo documentation. Move/copy it to `/docs/_legacy/...` with a legacy notice.
- Do not implement product code in this step.
- Do not approve ADRs in this step.
- Do not declare production readiness.
- Do not declare CI validated.
- Do not declare importability verified.
- Do not declare publish ready.
- Do not declare full behavioral equivalence.
- Do not treat Workbook as source/evidence/export/publish proof.
- Repo physical facts must come from repo discovery, not assumptions.
- Claims IBM ODM/BRE require IBM Docs, Real ODM validation, report/test, SME/Owner review, or explicit blocker.
- Future Devin sessions must start from `/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md` for any ODM V7 work.

## Target `/docs` structure

Create or update this structure:

```text
/docs/
  _legacy/
    odm-v7-target-architecture-pre-four-package-handoff-<YYYYMMDD>/
      LEGACY_NOTICE.md
      <previous ODM V7 target documentation preserved here>

  odm-v7-target-architecture/
    README.md
    IMPLEMENTATION_START_HERE.md
    DOCS_NAVIGATION_INDEX.md
    SOURCE_AUTHORITY_FOR_DEVIN.md

    00_source_packages/
      ZIP_FULL_POS_CLEANUP.zip
      ODM_CHATGPT_OPTIMIZED_SUPPORT_PACK.zip
      ODM_V7_DEVIN_OPERATIONAL_GUIDE_PACKAGE_REMEDIATED_FINAL_DEVIN_HANDOFF_CLEAN.zip
      ODM_V7_IMPLEMENTATION_PLAN_FINAL_DEVIN_AUTONOMY_UPDATE_REMEDIATED_FINAL_DEVIN_HANDOFF_CLEAN.zip
      SOURCE_PACKAGE_HASHES.md
      ODM_V7_RECONSTRUCTION_REPORT.md

    10_canonical_odm_documentation/
      <extracted contents of ZIP_FULL_POS_CLEANUP.zip preserving internal paths>

    20_chatgpt_optimized_support_pack/
      <extracted contents of ODM_CHATGPT_OPTIMIZED_SUPPORT_PACK.zip preserving internal paths>

    30_devin_operational_guide/
      <extracted contents of ODM_V7_DEVIN_OPERATIONAL_GUIDE_PACKAGE_REMEDIATED_FINAL_DEVIN_HANDOFF_CLEAN.zip preserving internal paths>

    40_implementation_plan/
      <extracted contents of ODM_V7_IMPLEMENTATION_PLAN_FINAL_DEVIN_AUTONOMY_UPDATE_REMEDIATED_FINAL_DEVIN_HANDOFF_CLEAN.zip preserving internal paths>

    90_migration_and_validation/
      DOCS_MIGRATION_REPORT.md
      REPO_REFERENCE_SCAN_RESULTS.md
      REFERENCE_UPDATE_REPORT.md
      FINAL_DOCS_INSTALL_VALIDATION_REPORT.md
      NAVIGATION_ENTRYPOINT_VALIDATION_REPORT.md
```

## Mandatory navigation entrypoints

Do not rely only on folder names. After installing the four packages, create these four entrypoint files at the root of `/docs/odm-v7-target-architecture/`:

```text
/docs/odm-v7-target-architecture/README.md
/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md
/docs/odm-v7-target-architecture/DOCS_NAVIGATION_INDEX.md
/docs/odm-v7-target-architecture/SOURCE_AUTHORITY_FOR_DEVIN.md
```

### `IMPLEMENTATION_START_HERE.md` requirements

This is the canonical first file for future Devin sessions and humans.

It must include:

1. A clear instruction: **for any ODM V7 task, start here**.
2. The absolute active documentation root: `/docs/odm-v7-target-architecture/`.
3. The four installed package areas and their roles.
4. The task startup procedure:
   - read `IMPLEMENTATION_START_HERE.md`;
   - read `SOURCE_AUTHORITY_FOR_DEVIN.md`;
   - use `DOCS_NAVIGATION_INDEX.md` to choose files;
   - use the support pack router for context minimization;
   - consult canonical ODM docs for architectural authority;
   - consult the operational guide for Devin execution protocol;
   - consult the implementation plan for phases/waves/slices.
5. The required first implementation phase: `P0.0 / N00 Repo Discovery`.
6. The rule that repo paths/classes/packages/scripts/commands must be discovered, not invented.
7. The project scope:
   - test repository scope;
   - no mandatory CI/CD pipeline;
   - no production deployment;
   - no production promotion;
   - no production release governance;
   - no production SLO/SLI/SLA/RTO/RPO;
   - no mandatory production observability;
   - no new formal secrets policy.
8. The non-removable gates:
   - Canonical ODM Model as current editable source of rules;
   - IBM ODM Real as external observable behavioral reference;
   - IBM Docs / Real ODM validation for IBM-specific claims;
   - Promotion Gate for candidate vs verified expected output;
   - no full behavioral equivalence claim;
   - Workbook is terminal human artifact, not source/evidence/export/publish proof.
9. A task routing table:
   - architecture question;
   - implementation planning;
   - implementation;
   - validation;
   - IBM ODM/BRE claim;
   - simulation/equivalence;
   - export/publish;
   - legacy migration;
   - Devin operation.
10. The expected first Devin output: `P0_0_N00_REPO_DISCOVERY_REPORT`.

### `DOCS_NAVIGATION_INDEX.md` requirements

This file must be a practical map, not a generic README.

It must include:

- Package-to-folder map.
- High-value files to start with in each folder.
- For the support pack, explicitly list:
  - `ODM_TASK_ROUTER.md`;
  - `ODM_SOURCE_AUTHORITY_MAP.md`;
  - `ODM_CONTEXT_PACK_MATRIX_COMPACT.csv`;
  - `ODM_STAGE_INDEX.md`;
  - `ODM_MINIMAL_RETRIEVAL_BUNDLES.md`;
  - `ODM_CLAIM_GUARDRAILS.md`.
- For the operational guide, explicitly list:
  - `00_MASTER_DEVIN_IMPLEMENTATION_GUIDE.md`;
  - `01_SOURCE_AUTHORITY_AND_INPUT_MAP.md`;
  - `02_IMPLEMENTATION_DAG_AND_DEPENDENCY_MATRIX.md`;
  - `05_SPECIALIST_SESSION_CARDS.md`;
  - `07_CONTRACT_SCHEMA_ARTIFACT_IMPACT_PROTOCOL.md`;
  - `09_IBM_ODM_EVIDENCE_AND_EXTERNAL_DOCS_PROTOCOL.md`;
  - `10_TEST_VALIDATION_AND_REVIEW_LOOP_PLAN.md`;
  - `12_FINAL_HANDOFF_TO_DEVIN.md`;
  - `13_PROMPTS_FOR_DEVIN_SESSIONS.md`;
  - `16_TASK_SOURCE_ROUTING_AND_CONTEXT_LOOKUP_MATRIX.md`;
  - `OWNER_SCOPE_DECISIONS_AND_OUT_OF_SCOPE_OPERATIONS.md`;
  - `NON_CI_VALIDATION_BASELINE.md`;
  - `OWNER_REVIEW_AND_DECISION_PROTOCOL.md`.
- For the implementation plan, explicitly list:
  - `00_IMPLEMENTATION_PLAN_STATUS_AND_STRATEGY.md`;
  - `03_REPO_DISCOVERY_AND_CHARACTERIZATION_PLAN.md`;
  - `05_CONTRACTS_SCHEMAS_AND_STATUS_REGISTRY_PLAN.md`;
  - `06_INCREMENTAL_IMPLEMENTATION_SLICES_P0_P1_P2.md`;
  - `07_COMPONENT_BUILDER_GATE_IMPLEMENTATION_SPECS.md`;
  - `08_TEST_VALIDATION_CI_QUALITY_GATE_PLAN.md`;
  - `10_IBM_REAL_ODM_EXPORT_IMPORTABILITY_EVIDENCE_PLAN.md`;
  - `11_FINAL_IMPLEMENTATION_PLAN_AND_HANDOFF.md`;
  - `15_DEVIN_AUTONOMY_AND_OWNER_OPERATING_BOUNDARY_UPDATE.md`;
  - `IMPLEMENTATION_PLAN_REQUIREMENT_EVIDENCE_INDEX.md`.
- A task-type-to-document routing table.
- A warning that `/docs/_legacy/` is never active target architecture.

### `SOURCE_AUTHORITY_FOR_DEVIN.md` requirements

This file must make authority unambiguous.

It must include:

1. Active documentation root: `/docs/odm-v7-target-architecture/`.
2. Legacy documentation root: `/docs/_legacy/...` for audit/history only.
3. Source hierarchy:
   - `ZIP_FULL_POS_CLEANUP.zip` extracted under `10_canonical_odm_documentation/` is the primary architectural source.
   - `ODM_CHATGPT_OPTIMIZED_SUPPORT_PACK.zip` extracted under `20_chatgpt_optimized_support_pack/` is derived routing/retrieval only.
   - The operational guide under `30_devin_operational_guide/` governs Devin execution and handoff operations.
   - The implementation plan under `40_implementation_plan/` governs implementation phases, slices, specs, gates and validation flow.
4. Conflict policy:
   - approved Decision Ledger/ADR if present;
   - `00_PROJECT_ESSENCE/`;
   - `20_ARCHITECTURE_CONTRACTS/`;
   - `30_IBM_ODM_KNOWLEDGE/`;
   - `10_ARCHITECTURE_OVERVIEW/`;
   - `40_DAG_AND_ROADMAP/`;
   - `60_IMPLEMENTABLE_ELEMENTS/`;
   - `50_ORCHESTRATORS/`;
   - `70_DEVIN_PLAYBOOKS/` and `80_PROMPT_LIBRARY/` only as derived execution material;
   - `45_LEGACY_MIGRATION_TO_TARGET/` only for legacy-to-target migration;
   - repo code only after repo discovery and with real path/command/evidence.
5. Non-authoritative materials:
   - legacy docs;
   - archive bundles;
   - patch logs;
   - transient reports;
   - prompt library alone;
   - summaries;
   - Documentation Artifact;
   - Devin Index, unless used only for known knowledge lookup and evidence routing.
6. Claim guardrails:
   - IBM ODM/BRE claims require evidence;
   - output equality does not prove full behavioral equivalence;
   - candidate expected output does not become verified expected output without Promotion Gate;
   - Workbook is terminal human artifact.

### `README.md` requirements

This should be concise and point to the three navigation files.

It must say:

```text
Start with IMPLEMENTATION_START_HERE.md for any ODM V7 task.
Use SOURCE_AUTHORITY_FOR_DEVIN.md for authority and conflict resolution.
Use DOCS_NAVIGATION_INDEX.md to find the right documents quickly.
```

## Documentation authority after installation

Use this operational authority sequence for every future ODM V7 task:

1. Start at `/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md`.
2. Use `/docs/odm-v7-target-architecture/SOURCE_AUTHORITY_FOR_DEVIN.md` to resolve authority and conflicts.
3. Use `/docs/odm-v7-target-architecture/DOCS_NAVIGATION_INDEX.md` to choose the minimum necessary documents.
4. Use `/docs/odm-v7-target-architecture/20_chatgpt_optimized_support_pack/` only for routing/retrieval.
5. Use `/docs/odm-v7-target-architecture/10_canonical_odm_documentation/` as the primary architectural source.
6. Use `/docs/odm-v7-target-architecture/30_devin_operational_guide/` for Devin operating protocol.
7. Use `/docs/odm-v7-target-architecture/40_implementation_plan/` for phases, waves, slices, specs, gates and validation.
8. Use legacy docs under `/docs/_legacy/` only for audit/history, never as active target architecture.

## Safe reconstruction script

Run this from the repository root after saving the container Markdown as:

`ODM_V7_FOUR_PACKAGES_UNIFIED_CONTAINER_FOR_DEVIN.md`

```python
from pathlib import Path
import base64
import hashlib
import json
import re
import zipfile

CONTAINER = Path("ODM_V7_FOUR_PACKAGES_UNIFIED_CONTAINER_FOR_DEVIN.md")
WORKDIR = Path("odm_v7_reconstruction_work")
ZIP_OUT = WORKDIR / "reconstructed_zips"
EXTRACT_OUT = WORKDIR / "extracted_for_validation"

def sha256_bytes(data: bytes) -> str:
    return hashlib.sha256(data).hexdigest()

def parse_kv(header: str) -> dict:
    meta = {}
    for line in header.splitlines():
        if ": " in line:
            k, v = line.split(": ", 1)
            meta[k.strip()] = v.strip()
    return meta

def safe_member_name(name: str) -> bool:
    if name.startswith("/") or name.startswith("\\"):
        return False
    if re.match(r"^[A-Za-z]:", name):
        return False
    parts = re.split(r"[\\/]+", name)
    return ".." not in parts

def safe_extract(zip_path: Path, dest: Path):
    dest.mkdir(parents=True, exist_ok=True)
    with zipfile.ZipFile(zip_path, "r") as z:
        for member in z.infolist():
            if not safe_member_name(member.filename):
                raise RuntimeError(f"Unsafe ZIP path blocked: {member.filename}")
        z.extractall(dest)

text = CONTAINER.read_text(encoding="utf-8")
WORKDIR.mkdir(parents=True, exist_ok=True)
ZIP_OUT.mkdir(parents=True, exist_ok=True)
EXTRACT_OUT.mkdir(parents=True, exist_ok=True)

zip_blocks = re.findall(
    r"===== BEGIN ODM_V7_ZIP_PACKAGE =====\n(.*?)----- BEGIN ZIP_BASE64 -----\n(.*?)\n----- END ZIP_BASE64 -----\n(.*?)===== END ODM_V7_ZIP_PACKAGE =====",
    text,
    flags=re.S,
)
if len(zip_blocks) != 4:
    raise RuntimeError(f"Expected 4 ZIP blocks, found {len(zip_blocks)}")

manifest = {"reconstructed": [], "file_audit": []}

for before, b64, after in zip_blocks:
    meta = parse_kv(before + "\n" + after)
    canonical = meta["CANONICAL_FILENAME"]
    expected_sha = meta["ZIP_SHA256"]
    expected_size = int(meta["ZIP_SIZE_BYTES"])
    data = base64.b64decode("".join(b64.split()))
    actual_sha = sha256_bytes(data)
    if actual_sha != expected_sha:
        raise RuntimeError(f"SHA mismatch for {canonical}: {actual_sha} != {expected_sha}")
    if len(data) != expected_size:
        raise RuntimeError(f"Size mismatch for {canonical}: {len(data)} != {expected_size}")
    out = ZIP_OUT / canonical
    out.write_bytes(data)
    with zipfile.ZipFile(out, "r") as z:
        bad = z.testzip()
        if bad is not None:
            raise RuntimeError(f"ZIP integrity failure in {canonical} at {bad}")
    manifest["reconstructed"].append({
        "package_id": meta["PACKAGE_ID"],
        "canonical_filename": canonical,
        "sha256": actual_sha,
        "size_bytes": len(data),
        "file_count": int(meta["ZIP_FILE_COUNT"]),
    })

file_blocks = re.findall(
    r"===== BEGIN ODM_V7_INTERNAL_FILE =====\n(.*?)----- BEGIN FILE_BASE64 -----\n(.*?)\n----- END FILE_BASE64 -----\n(.*?)===== END ODM_V7_INTERNAL_FILE =====",
    text,
    flags=re.S,
)
if not file_blocks:
    raise RuntimeError("No internal file audit blocks found.")

for item in manifest["reconstructed"]:
    safe_extract(ZIP_OUT / item["canonical_filename"], EXTRACT_OUT / item["package_id"])

for before, b64, after in file_blocks:
    meta = parse_kv(before + "\n" + after)
    pkg = meta["PACKAGE_ID"]
    internal_path = meta["ZIP_INTERNAL_PATH"]
    expected_sha = meta["FILE_SHA256"]
    expected_size = int(meta["FILE_SIZE_BYTES"])
    payload = base64.b64decode("".join(b64.split()))
    if sha256_bytes(payload) != expected_sha:
        raise RuntimeError(f"Internal FILE_BASE64 SHA mismatch: {pkg} :: {internal_path}")
    if len(payload) != expected_size:
        raise RuntimeError(f"Internal FILE_BASE64 size mismatch: {pkg} :: {internal_path}")
    extracted_file = EXTRACT_OUT / pkg / internal_path
    if not extracted_file.exists():
        raise RuntimeError(f"Extracted file missing: {pkg} :: {internal_path}")
    extracted = extracted_file.read_bytes()
    if extracted != payload:
        raise RuntimeError(f"Extracted content mismatch: {pkg} :: {internal_path}")
    manifest["file_audit"].append({
        "package_id": pkg,
        "zip_internal_path": internal_path,
        "sha256": expected_sha,
        "size_bytes": expected_size,
    })

(WORKDIR / "RECONSTRUCTION_VALIDATION_MANIFEST.json").write_text(
    json.dumps(manifest, indent=2, ensure_ascii=False),
    encoding="utf-8",
)
print("RECONSTRUCTION_VALIDATION_PASS")
print(json.dumps({
    "zip_count": len(manifest["reconstructed"]),
    "file_audit_count": len(manifest["file_audit"]),
}, indent=2))
```

## Installation protocol

After the script prints `RECONSTRUCTION_VALIDATION_PASS`:

1. Create `/docs/odm-v7-target-architecture/`.
2. Preserve any previous ODM V7 target documentation under:
   `/docs/_legacy/odm-v7-target-architecture-pre-four-package-handoff-<YYYYMMDD>/`.
3. Copy the four reconstructed ZIPs into:
   `/docs/odm-v7-target-architecture/00_source_packages/`.
4. Extract the packages as follows:
   - `ZIP_FULL_POS_CLEANUP.zip` → `/docs/odm-v7-target-architecture/10_canonical_odm_documentation/`
   - `ODM_CHATGPT_OPTIMIZED_SUPPORT_PACK.zip` → `/docs/odm-v7-target-architecture/20_chatgpt_optimized_support_pack/`
   - `ODM_V7_DEVIN_OPERATIONAL_GUIDE_PACKAGE_REMEDIATED_FINAL_DEVIN_HANDOFF_CLEAN.zip` → `/docs/odm-v7-target-architecture/30_devin_operational_guide/`
   - `ODM_V7_IMPLEMENTATION_PLAN_FINAL_DEVIN_AUTONOMY_UPDATE_REMEDIATED_FINAL_DEVIN_HANDOFF_CLEAN.zip` → `/docs/odm-v7-target-architecture/40_implementation_plan/`
5. Generate:
   - `/docs/odm-v7-target-architecture/README.md`
   - `/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md`
   - `/docs/odm-v7-target-architecture/DOCS_NAVIGATION_INDEX.md`
   - `/docs/odm-v7-target-architecture/SOURCE_AUTHORITY_FOR_DEVIN.md`
   - `/docs/odm-v7-target-architecture/00_source_packages/SOURCE_PACKAGE_HASHES.md`
   - `/docs/odm-v7-target-architecture/00_source_packages/ODM_V7_RECONSTRUCTION_REPORT.md`
   - `/docs/odm-v7-target-architecture/90_migration_and_validation/DOCS_MIGRATION_REPORT.md`
   - `/docs/odm-v7-target-architecture/90_migration_and_validation/NAVIGATION_ENTRYPOINT_VALIDATION_REPORT.md`
6. Validate that all four navigation files exist and explicitly reference each other.
7. Validate that `IMPLEMENTATION_START_HERE.md` points to the correct active root and first phase `P0.0 / N00 Repo Discovery`.
8. Validate that no active entrypoint points to `/docs/_legacy/` as active target architecture.

## Repository-wide reference migration

Scan the entire repository for references to superseded ODM V7 documentation.

Minimum search targets:

```text
AGENTS.md
agents.md
.agent*
.devin*
skills
skill
playbooks
prompt
prompts
knowledge
knowledge_sources
source
sources
docs
documentation
ODM V7
odm-v7
ZIP_FULL_POS_CLEANUP
ODM_CHATGPT_OPTIMIZED_SUPPORT_PACK
DEVIN_OPERATIONAL_GUIDE
IMPLEMENTATION_PLAN
architecture-target
target architecture
Canonical ODM Model
```

Recommended commands, adapted to the actual repo tools:

```bash
git status --short
find . -maxdepth 4 -iname '*agent*' -o -iname '*skill*' -o -iname '*playbook*' -o -iname '*knowledge*' -o -iname '*prompt*'
rg -n "ODM V7|odm-v7|ZIP_FULL_POS_CLEANUP|ODM_CHATGPT_OPTIMIZED_SUPPORT_PACK|DEVIN_OPERATIONAL_GUIDE|IMPLEMENTATION_PLAN|architecture-target|target architecture|Canonical ODM Model|knowledge sources|playbooks|skills|AGENTS\.md|IMPLEMENTATION_START_HERE|DOCS_NAVIGATION_INDEX|SOURCE_AUTHORITY_FOR_DEVIN" .
```

Update references so future Devin work uses this canonical entrypoint:

```text
/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md
```

and no longer treats the legacy ODM V7 docs as the active target architecture.

Mandatory external reference updates:

- If `AGENTS.md` or `agents.md` exists, update it to say: for ODM V7 work, start at `/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md`.
- If Devin skills exist, update ODM-related skills to point to the new entrypoint and source authority file.
- If knowledge sources exist, update ODM V7 source paths to the new `/docs/odm-v7-target-architecture/` tree.
- If playbooks/prompts exist, update references to legacy docs or old package names.
- If any reference should not be changed, record why in `REFERENCE_UPDATE_REPORT.md`.

Do not mass-edit blindly. For every changed file, record:

- file path;
- old reference;
- new reference;
- reason;
- validation performed.

## Final validation protocol

Before returning, validate:

- four ZIPs reconstructed with exact SHA-256 match;
- internal file audit count matches the container;
- unsafe ZIP paths count is zero;
- `/docs/odm-v7-target-architecture/README.md` exists;
- `/docs/odm-v7-target-architecture/IMPLEMENTATION_START_HERE.md` exists;
- `/docs/odm-v7-target-architecture/DOCS_NAVIGATION_INDEX.md` exists;
- `/docs/odm-v7-target-architecture/SOURCE_AUTHORITY_FOR_DEVIN.md` exists;
- each navigation file links or names the other three;
- repository-wide references to active ODM V7 docs point to the new entrypoint or root;
- legacy docs are preserved under `/docs/_legacy/` and are not referenced as active target architecture;
- no product code was implemented.

## Expected final output from Devin

Return:

`ODM_V7_DOCS_RECONSTRUCTION_AND_INSTALL_REPORT`

Include:

- reconstructed ZIPs and SHA-256 hashes;
- ZIP integrity results;
- per-file audit result count;
- final `/docs` tree;
- generated navigation entrypoints and one-paragraph summary of each;
- legacy docs location;
- reference scan commands and results;
- files updated outside `/docs`;
- files intentionally not updated and why;
- blockers;
- Owner Review needs;
- final GO/NO-GO for starting `P0.0 / N00 Repo Discovery`.
