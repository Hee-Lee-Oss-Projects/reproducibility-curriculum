# TASKS — reproducibility-curriculum

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## How these tasks map to Hee-Lee Oss

Each task below becomes a Hee-Lee Oss **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- `id` — stable slug ID from the tables (e.g. `reproducibility-curriculum-framework-001`).
- `title` — the table's Title.
- `project` — `reproducibility-curriculum`.
- `type` — one of `code | research | writing | data | design-spec | maintenance` (see each table).
- `lane` — `donated` for all tasks here (no funded escrow). A funded task would add `fundedBudgetUsd`.
- `priority` — `high | medium | low`.
- `domain` — array, e.g. `["cancer-research","open-science","education","reproducibility"]`.
- `riskTier` — `low | medium | high`. Pure-pedagogy tasks are `low`; tasks that **touch a real open
  cancer dataset** are `medium` (force domain + Data&licensing review). **No `high` tasks** —
  patient-facing content is out of scope.
- `urgent` — boolean; `false` for all current tasks.
- `deliverable` — `pr | dataset | document | translation`. We **never** deliver `dataset` (data is out
  of scope); code/containers → `pr`; lessons/specs/checklists → `document`; localized module →
  `translation`.
- `tokenEstimate` — `small | medium | large` (Size column).
- `status` — `open | in-progress | review | delivered | done`; all start `open`.
- `context`, `objective`, `acceptanceCriteria[]`, `resources[]`, `output` — per task.
- `requestor` — `TO BE SECURED` until a teaching/adoption partner is confirmed.
- `verifiedNeed` — **`false`** until a named program/core/cohort agrees to teach or adopt the
  curriculum (general need is real; per-task delivery need is unproven).
- `outputLicense` — `CC-BY-4.0` for instructional content; `MIT` for code/container recipes.

---

## Milestone M0 — Foundation & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| reproducibility-curriculum-framework-001 | Curriculum framework + Bloom-aligned competency map (backward design) | design-spec | small | low | document | — | Educator |
| reproducibility-curriculum-datagate-002 | Open-cancer-data & licensing/identifiability gate + DATASET-CATALOG.md | design-spec | medium | medium | document | — | Data & licensing |
| reproducibility-curriculum-reviewers-003 | Name/secure blocking reviewers (Data&licensing, domain, educator) | research | small | low | document | — | Maintainer |
| reproducibility-curriculum-template-004 | Module template + style/accessibility guide (WCAG 2.2 AA, i18n-ready) | design-spec | small | low | document | framework-001 | Educator |
| reproducibility-curriculum-container-ci-005 | Container build/test CI harness + base-image pinning policy (Docker + Apptainer) | code | medium | low | pr | template-004 | Technical |
| reproducibility-curriculum-pilot-006 | Pilot module end-to-end: "Containers & environments" + 1 gated worked example | writing | large | medium | document | framework-001, datagate-002, template-004, container-ci-005, reviewers-003 | Data & licensing, Domain, Educator, Technical |
| reproducibility-curriculum-outreach-007 | Partner/cohort outreach + pilot teaching plan | research | small | low | document | — | Steward |

**Acceptance criteria — key tasks**

- **framework-001 (curriculum framework + competency map)**
  - [ ] Six modules (A motivation, B versioning, C provenance, D containers, E reproducible analysis,
        F sharing/archiving) + capstone defined with scope boundaries.
  - [ ] Each module has 3–6 **measurable, Bloom-aligned** learning objectives derived by backward
        design (objective → assessment → content).
  - [ ] Explicitly methodological-only: no clinical/medical-advice content; examples never present a
        biological/clinical conclusion as a finding.
  - [ ] Content licensed CC-BY-4.0; code/containers MIT; stated in the framework.

- **datagate-002 (open-cancer-data & licensing/identifiability gate)** *(headline gate)*
  - [ ] Encodes the binding guardrail: **open-access/aggregate/de-identified ONLY**; dbGaP/EGA/
        controlled-access/individual-level/identifiable data **categorically DENIED**.
  - [ ] Objective PASS criterion: license on the ALLOW list **and** `license.permitsDerivatives: true`
        with cited clause/URL **and** `identifiability: none|aggregate|deidentified`. Missing evidence,
        non-commercial terms, controlled access, or any identifiability signal = FLAG/EXCLUDE.
  - [ ] `DATASET-CATALOG.md` created with ALLOW (GDC open tier, DepMap CC-BY 4.0, GEO/SRA per-series,
        cBioPortal public, ICGC open, Ensembl, gnomAD, synthetic), **FLAG** (COSMIC, OncoKB — NC,
        excluded as example data), **DENY** (dbGaP, EGA, controlled/identifiable).
  - [ ] Requires recording source URL + version + retrieval date + license id/URL + snapshot
        (committed copy + SHA-256 + Wayback URL) + identifiability classification + attribution.
  - [ ] Produces a committed, reviewable PASS/FLAG/EXCLUDE artifact per dataset; a CI catalog
        validator asserts every example references only a PASS entry.

- **container-ci-005 (container CI harness)**
  - [ ] Builds each recipe from a base image **pinned by digest**; pins package versions
        (conda/mamba env with explicit versions / lockfile).
  - [ ] Produces both a `Dockerfile` and an **Apptainer/Singularity** definition that build and pass a
        smoke test; scheduled rebuild detects upstream drift and marks lessons stale.
  - [ ] Wires in the dataset-catalog validator, link/citation checker, and executable-example render
        (Quarto/papermill) as CI steps.
  - [ ] Code MIT; `pnpm build && pnpm test && pnpm lint` green for repo tooling; DCO signed-off; no
        secrets embedded.

- **pilot-006 (pilot module end-to-end)**
  - [ ] "Containers & environments" module complete to the template: objectives, lesson (all
        assertions cited), runnable exercise, one **gated** worked example, checklist, assessment,
        instructor notes.
  - [ ] Worked example uses the **lowest-risk allowed source** (DepMap CC-BY 4.0 or fully synthetic),
        with a committed PASS gate artifact; data fetched at runtime, none committed.
  - [ ] Container builds (Docker + Apptainer) and exercise/example pass in CI (green in last run).
  - [ ] Signed off by Data & licensing, Domain, Educator, and Technical reviewers.
  - [ ] **Taught or self-delivered** to ≥ 1 learner/cohort (self-run workshop fallback acceptable) with
        the outcome recorded in the ledger — or, if no learner yet, marked delivered-pending with the
        blocker surfaced.

**M0 Definition of Done:** blocking reviewers named (before pilot review); framework + competency map,
module template (WCAG 2.2 AA, i18n-ready), and the **open-cancer-data & licensing gate** +
`DATASET-CATALOG.md` published; container CI harness green (Docker + Apptainer) with catalog/link/
render checks wired in; the pilot "Containers" module complete, gated, CI-green, and reviewed; ≥ 1
partner/cohort-outreach thread opened.

---

## Milestone M1 — Core skill modules

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| reproducibility-curriculum-versioning-008 | "Versioning" module (git, data/protocol versioning, DOIs) | writing | medium | low | document | template-004, container-ci-005 | Educator, Technical |
| reproducibility-curriculum-provenance-009 | "Provenance" module (FAIR, RO-Crate, ISA, ELN concepts) | writing | medium | low | document | template-004, container-ci-005 | Educator, Domain |
| reproducibility-curriculum-analysis-010 | "Reproducible analysis" module (literate programming, seeds, pinning) | writing | medium | medium | document | template-004, container-ci-005, datagate-002 | Educator, Data & licensing, Technical |
| reproducibility-curriculum-assessment-011 | Pre/post competency assessment instrument + rubric | design-spec | small | low | document | framework-001 | Educator |
| reproducibility-curriculum-checklist-012 | Reproducibility checklist + data/code-availability statement template | writing | small | low | document | framework-001 | Domain, Educator |
| reproducibility-curriculum-a11y-013 | Accessibility + i18n-readiness pass on published modules (WCAG 2.2 AA) | maintenance | small | low | document | pilot-006, versioning-008, provenance-009 | Educator |

**Acceptance criteria — key tasks**

- **analysis-010 (reproducible-analysis module)**
  - [ ] Teaches literate programming (Quarto/R Markdown/Jupyter), seed setting, and dependency pinning
        with a runnable, CI-rendered example.
  - [ ] Any worked example using a real dataset has a committed PASS gate artifact (`datagate-002`);
        data fetched at runtime in bounded slices, none committed (hence `riskTier: medium`).
  - [ ] Example is methodological — no biological/clinical conclusion presented as a finding.

- **assessment-011 (competency assessment)**
  - [ ] Items map 1:1 to the framework's learning objectives (containers, provenance, versioning).
  - [ ] Parallel pre/post forms enabling a **normalized-gain** computation `g=(post−pre)/(max−pre)`.
  - [ ] Reviewed by the educator reviewer for construct validity; scoring key included.

- **checklist-012 (reproducibility checklist + availability statement)**
  - [ ] A concise, reusable reproducibility checklist learners keep, aligned to module objectives.
  - [ ] A fill-in data/code-availability statement template referencing open-archiving options
        (Zenodo/GEO/SRA/OSF) and licensing (CC-BY-4.0/MIT).

**M1 Definition of Done:** versioning, provenance, and reproducible-analysis modules published and
green in CI (each with a gated worked example or synthetic exercise); pre/post assessment instrument
reviewed for validity; reproducibility checklist + availability-statement template published;
accessibility pass (WCAG 2.2 AA) complete on all published modules.

---

## Milestone M2 — Worked examples, capstone & first taught cohort

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| reproducibility-curriculum-sharing-014 | "Sharing & archiving" module (Zenodo, GEO/SRA, protocols.io, OSF) | writing | medium | low | document | template-004, container-ci-005 | Educator, Domain |
| reproducibility-curriculum-examples-015 | ≥ 3 gated worked examples on distinct open cancer datasets | writing | large | medium | document | datagate-002, analysis-010, provenance-009 | Data & licensing, Domain, Technical |
| reproducibility-curriculum-capstone-016 | Capstone: make a small open-cancer-data analysis fully reproducible | code | large | medium | pr | datagate-002, analysis-010, checklist-012, container-ci-005 | Data & licensing, Domain, Technical |
| reproducibility-curriculum-cohort-017 | Teach a pilot cohort + capture pre/post outcomes | research | medium | low | document | pilot-006, assessment-011, outreach-007 | Steward, Educator |

**Acceptance criteria — key tasks**

- **examples-015 (gated worked examples)**
  - [ ] ≥ 3 worked examples across distinct **open** cancer datasets (e.g. DepMap, a GDC/TCGA open-tier
        summary, a public GEO series), each with a committed PASS gate artifact (`permitsDerivatives:
        true`, non-identifiable).
  - [ ] Each example fetches at runtime in bounded slices; **no raw data committed**; renders in CI.
  - [ ] Each is methodological and labeled "teaching example — not a finding, not advice."

- **capstone-016 (authentic-assessment capstone)**
  - [ ] Learners take a small open-cancer-data analysis and produce a fully reproducible artifact:
        pinned container + literate analysis + provenance + data/code-availability statement.
  - [ ] Graded against the `checklist-012` rubric; reference solution builds and re-runs green in CI.
  - [ ] Source dataset has a committed PASS gate artifact; no data committed (`riskTier: medium`).

- **cohort-017 (first taught cohort)**
  - [ ] ≥ 1 cohort taught (workshop or embedded course); pre/post assessment captured (baseline +
        post) and recorded in the outcome ledger.
  - [ ] ≥ 1 learner-produced reproducible artifact verified (public repo/DOI that builds and re-runs).
  - [ ] If a partner taught it, relevant tasks updated to `verifiedNeed: true` with `requestor` set.

**M2 Definition of Done:** sharing/archiving module + capstone published and green; ≥ 3 gated worked
examples on distinct open cancer datasets; ≥ 1 cohort taught with pre/post captured; ≥ 1 verified
learner-produced reproducible artifact recorded in the ledger.

---

## Milestone M3 — Scale, train-the-trainer & sustainability

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| reproducibility-curriculum-trainer-018 | Instructor guide + train-the-trainer kit | writing | medium | low | document | cohort-017 | Educator, Steward |
| reproducibility-curriculum-refresh-019 | Container/dependency refresh process + staleness pipeline | maintenance | small | low | document | container-ci-005 | Maintainer, Technical |
| reproducibility-curriculum-adopt-020 | Secure ≥ 1 external adopter + record adoption evidence | research | small | low | document | trainer-018, cohort-017 | Steward |
| reproducibility-curriculum-i18n-021 | Localize one core module (domain-qualified reviewer) | translation | medium | medium | translation | template-004, versioning-008 | Domain, Educator |

**Acceptance criteria — key tasks**

- **trainer-018 (train-the-trainer kit)**
  - [ ] Instructor guide covering setup, timing, common misconceptions, and accessibility per module.
  - [ ] A reusable train-the-trainer package (slides/notes/checklists) enabling a new instructor to
        teach the curriculum without the original authors.

- **adopt-020 (external adopter)**
  - [ ] A named third party teaches or embeds the curriculum (syllabus reference / scheduled run /
        taught fork), evidenced by a verifiable link/record in the outcome ledger.
  - [ ] Tasks for that adopter updated to `verifiedNeed: true` with `requestor` set.

**M3 Definition of Done:** instructor + train-the-trainer kit published; ≥ 1 external adopter confirmed
with evidence; container/dependency refresh process documented and a steward identified; ≥ 1 module
localized via a domain-qualified reviewer; cumulative success-metric targets met.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| reproducibility-curriculum-workflows-022 | Advanced module: workflow managers (Nextflow/Snakemake) | writing | large | medium | document | Deferred from M1; conceptual intro only in core |
| reproducibility-curriculum-screencasts-023 | Screencasts/video walkthroughs with captions | writing | medium | low | document | Accessibility: captions + transcripts required |
| reproducibility-curriculum-carpentries-024 | Port to The Carpentries Incubator lesson format | code | medium | low | pr | If Carpentries adoption path is chosen |
| reproducibility-curriculum-dashboard-025 | Outcome dashboard (cohorts, artifacts, adoptions) | code | medium | low | pr | Reads the outcome ledger; supports metric tracking |
| reproducibility-curriculum-i18n-batch-026 | Localize remaining modules (per-language domain reviewer) | translation | large | medium | translation | Scales i18n-021 once one localization proves out |

---

## Example task JSON

```json
{
  "id": "reproducibility-curriculum-framework-001",
  "title": "Curriculum framework + Bloom-aligned competency map (backward design)",
  "project": "reproducibility-curriculum",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["cancer-research", "open-science", "education", "reproducibility"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "small",
  "status": "open",
  "context": "Wet-lab and translational cancer scientists are rarely taught versioning, provenance, or reproducible compute, and a meaningful fraction of preclinical cancer findings fail to replicate. Before any module is authored, the project needs a coherent framework and a Bloom-aligned competency map so every later module, assessment, and worked example aligns by backward design. The curriculum is methodological and for scientists, not patients: it contains no medical advice and presents no example result as a biological or clinical finding. Worked examples will use only open-access/aggregate/de-identified cancer data behind a binding licensing gate.",
  "objective": "Define the six-module curriculum (motivation, versioning, provenance, containers/environments, reproducible analysis, sharing/archiving) plus a capstone, each with measurable, Bloom-aligned learning objectives derived by backward design, and fix the dual-licensing and methodological-only scope boundaries.",
  "acceptanceCriteria": [
    "Six modules plus capstone are defined with explicit scope boundaries and sequencing/dependencies.",
    "Each module has 3-6 measurable, Bloom-aligned learning objectives produced by backward design (objective -> assessment -> content).",
    "The framework states the methodological-only boundary: no medical advice, no patient-facing content, and no example result presented as a biological/clinical finding.",
    "The framework states dual licensing: instructional content CC-BY-4.0, code/container recipes MIT.",
    "The framework references the binding open-cancer-data & licensing gate and notes that worked examples use only open/aggregate/de-identified data with provenance on every assertion.",
    "Document is accessible (plain language, heading structure) and i18n-ready; committed with DCO sign-off."
  ],
  "resources": [
    "C:\\code\\hee-lee-oss\\planning\\projects\\reproducibility-curriculum\\PLAN.md",
    "C:\\code\\hee-lee-oss\\docs\\good-deed-definition.md",
    "C:\\code\\hee-lee-oss\\planning\\ROADMAP.md",
    "The Turing Way (reproducible, ethical, collaborative data science)",
    "Bloom's taxonomy (revised); Understanding by Design (Wiggins & McTighe)",
    "NIH Rigor & Reproducibility guidance; Reproducibility Project: Cancer Biology"
  ],
  "output": "A curriculum framework document plus a Bloom-aligned competency/learning-objective map covering six modules and a capstone, committed to the project repo as the basis for the module template and all later modules.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```

---

## Backlog rollup

- **21 scheduled tasks** across M0–M3 (M0: 7 · M1: 6 · M2: 4 · M3: 4) + **5 backlog** tasks = **26**.
- By risk: **low: 18** · **medium: 8** (every dataset-touching task) · **high: 0** (patient-facing is
  out of scope — no high-risk tasks by design).
- By deliverable: `document` (lessons/specs/checklists), `pr` (CI harness, capstone code, dashboards),
  `translation` (localization). **No `dataset` deliverables** — data is never produced or republished.
- All tasks `lane: donated`, `verifiedNeed: false`, `requestor: TO BE SECURED` until a named
  teaching/adoption partner confirms — at which point that partner's tasks flip to `verifiedNeed: true`.

---

## Generated task index

> Auto-generated by Hee-Lee Oss task-decomposition agent — 2026-06-29.
> 26 schema-valid `tasks/*.json` files; seed (001) kept; 25 new files generated.
> Validation: ALL VALID (node validate-tasks.mjs, 26/26).

| File | ID | Title | Type | Deliverable | Risk | Priority | Token |
| --- | --- | --- | --- | --- | --- | --- | --- |
| framework-001.json | reproducibility-curriculum-framework-001 | Curriculum framework + Bloom-aligned competency map | design-spec | document | low | high | small |
| datagate-002.json | reproducibility-curriculum-datagate-002 | Open-cancer-data & licensing/identifiability gate + DATASET-CATALOG.md | design-spec | document | medium | high | medium |
| reviewers-003.json | reproducibility-curriculum-reviewers-003 | Name/secure blocking reviewers | research | document | low | high | small |
| template-004.json | reproducibility-curriculum-template-004 | Module template + style/accessibility guide | design-spec | document | low | high | small |
| container-ci-005.json | reproducibility-curriculum-container-ci-005 | Container build/test CI harness + base-image pinning policy | code | pr | low | high | medium |
| pilot-006.json | reproducibility-curriculum-pilot-006 | Pilot module end-to-end: "Containers & environments" | writing | document | medium | high | large |
| outreach-007.json | reproducibility-curriculum-outreach-007 | Partner/cohort outreach + pilot teaching plan | research | document | low | high | small |
| versioning-008.json | reproducibility-curriculum-versioning-008 | "Versioning" module (git, data/protocol versioning, DOIs) | writing | document | low | high | medium |
| provenance-009.json | reproducibility-curriculum-provenance-009 | "Provenance" module (FAIR, RO-Crate, ISA, ELN concepts) | writing | document | low | high | medium |
| analysis-010.json | reproducibility-curriculum-analysis-010 | "Reproducible analysis" module (literate programming, seeds, pinning) | writing | document | medium | high | medium |
| assessment-011.json | reproducibility-curriculum-assessment-011 | Pre/post competency assessment instrument + rubric | design-spec | document | low | high | small |
| checklist-012.json | reproducibility-curriculum-checklist-012 | Reproducibility checklist + data/code-availability statement template | writing | document | low | high | small |
| a11y-013.json | reproducibility-curriculum-a11y-013 | Accessibility + i18n-readiness pass on published modules | maintenance | document | low | high | small |
| sharing-014.json | reproducibility-curriculum-sharing-014 | "Sharing & archiving" module (Zenodo, GEO/SRA, protocols.io, OSF) | writing | document | low | medium | medium |
| examples-015.json | reproducibility-curriculum-examples-015 | >= 3 gated worked examples on distinct open cancer datasets | writing | document | medium | medium | large |
| capstone-016.json | reproducibility-curriculum-capstone-016 | Capstone: make a small open-cancer-data analysis fully reproducible | code | pr | medium | medium | large |
| cohort-017.json | reproducibility-curriculum-cohort-017 | Teach a pilot cohort + capture pre/post outcomes | research | document | low | medium | medium |
| trainer-018.json | reproducibility-curriculum-trainer-018 | Instructor guide + train-the-trainer kit | writing | document | low | medium | medium |
| refresh-019.json | reproducibility-curriculum-refresh-019 | Container/dependency refresh process + staleness pipeline | maintenance | document | low | medium | small |
| adopt-020.json | reproducibility-curriculum-adopt-020 | Secure >= 1 external adopter + record adoption evidence | research | document | low | medium | small |
| i18n-021.json | reproducibility-curriculum-i18n-021 | Localize one core module (domain-qualified reviewer) | writing | translation | medium | medium | medium |
| workflows-022.json | reproducibility-curriculum-workflows-022 | Advanced module: workflow managers (Nextflow/Snakemake) | writing | document | medium | low | large |
| screencasts-023.json | reproducibility-curriculum-screencasts-023 | Screencasts/video walkthroughs with captions | writing | document | low | low | medium |
| carpentries-024.json | reproducibility-curriculum-carpentries-024 | Port to The Carpentries Incubator lesson format | code | pr | low | low | medium |
| dashboard-025.json | reproducibility-curriculum-dashboard-025 | Outcome dashboard (cohorts, artifacts, adoptions) | code | pr | low | low | medium |
| i18n-batch-026.json | reproducibility-curriculum-i18n-batch-026 | Localize remaining modules (per-language domain reviewer) | writing | translation | medium | low | large |
