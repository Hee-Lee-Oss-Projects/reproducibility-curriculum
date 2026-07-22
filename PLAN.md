# PLAN — reproducibility-curriculum

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## Executive summary

Wet-lab and translational cancer scientists routinely produce results that are difficult or
impossible for anyone — including their own future selves — to reproduce: analyses run in
undocumented, hand-built software environments; figures whose generating code and inputs are lost;
protocols and data tracked in ad-hoc spreadsheets with no version history; and "data/code available
on request" statements that resolve to nothing. The cost is borne by patients: a meaningful fraction
of preclinical cancer findings do not replicate, slowing the translation of real discoveries into
therapies and wasting scarce research funding. The skills that fix this — **versioning, provenance,
and computational reproducibility (containers/environments)** — are rarely taught to bench
scientists, who are not primarily computational and are poorly served by tutorials written for
software engineers.

This project produces an **open, hands-on curriculum** that teaches reproducibility to wet-lab and
translational cancer researchers: short lessons, runnable container-based exercises, worked examples
on **open cancer data only**, reusable checklists/templates (reproducibility checklist, data/code
availability statement, environment recipe), pre/post competency assessments, and instructor
("train-the-trainer") materials. The pedagogy follows established practice — **backward design with
Bloom-aligned learning objectives**, and **Carpentries-style** formative assessment and live coding.
Output is **CC-BY-4.0** for instructional content and **MIT** for code/container recipes.

The deliverable is **teaching material, not data and not medical advice.** Every worked example uses
only **open-access / aggregate / de-identified** cancer data whose license is verified to permit
reuse and derivatives; controlled-access and identifiable patient data are categorically out of
scope. The curriculum is methodological — it teaches *how to make an analysis reproducible*, never
*what a result means clinically* — and is for scientists, not patients, so patient-facing content is
out of scope entirely. Every factual assertion in the lessons (including the motivating
"reproducibility crisis" claims) is sourced.

Overall **risk tier is low.** The two real risks are not pedagogical but (1) **licensing/data
governance** — letting a non-open or identifiable dataset into an example — and (2) **bit-rot** —
"runnable" exercises that silently stop building. The plan front-loads a binding **open-cancer-data
& licensing gate** and a **container CI harness** so both risks are controlled by automation and
review rather than good intentions.

## Problem & beneficiaries

**Who is helped.**
- **Primary:** wet-lab and translational cancer researchers (PhD students, postdocs, staff
  scientists, PIs) who generate or lightly analyze data — RNA-seq/qPCR, flow, imaging, screens — but
  have no formal training in versioning, provenance, or reproducible compute. They are the learners.
- **Secondary:** the **beneficiaries of the science** — patients and the field — who gain when
  cancer results are reproducible, reusable, and faster to translate. Reproducible methods are a
  precondition for trustworthy preclinical research.
- **Institutional:** cancer-center bioinformatics cores, graduate programs, and training facilities
  that need ready-to-teach, domain-relevant material and currently improvise it.

**The verified need.** The *general* need is well established and externally documented: the
Reproducibility Project: Cancer Biology and multiple surveys report that a large share of
preclinical cancer findings fail to replicate, and funders (NIH rigor & reproducibility guidance,
journal data/code-availability mandates) now require practices most bench scientists were never
taught. We treat the general need as real. The **specific, per-cohort need is TO BE SECURED**: we
have not yet confirmed a named training program, core facility, or cohort that has agreed to adopt
or teach this curriculum. Until a named partner commits to teach/adopt it, tasks carry
`verifiedNeed: false`, because "delivered, not merged" requires the material to actually be taught
to and used by learners, not merely written.

**Partner org.** TO BE SECURED. Candidate channels: cancer-center bioinformatics/training cores,
graduate program directors, The Carpentries (Incubator / Software & Data Carpentry lesson program),
ELIXIR / Bioinformatics training networks, The Turing Way community, pediatric-sarcoma and other
disease-focused research consortia. M0 includes explicit partner/cohort outreach; no partner is
assumed.

## Goals and non-goals

**Goals**
- Produce a coherent, modular curriculum with **measurable, Bloom-aligned learning objectives**
  covering: motivation, **versioning**, **provenance**, **containers/environments**, reproducible
  analysis, and sharing/archiving.
- Make every hands-on exercise **runnable and CI-verified** — container recipes that build and pass
  tests on a schedule, so "reproducible" is demonstrated, not asserted.
- Use **only open cancer data** in worked examples, behind a binding licensing/data-governance gate,
  with provenance and attribution recorded for every dataset and every claim.
- Provide reusable, durable artifacts learners keep: a **reproducibility checklist**, a
  **data/code-availability statement template**, and **environment recipe templates**.
- Provide **pre/post competency assessments** so the project measures behavior change, not pages
  written.
- Provide **instructor / train-the-trainer** materials so adoption scales beyond the authors.
- Be **accessible** (WCAG 2.2 AA) and **i18n-ready** so the material can be localized later cheaply.

**Non-goals**
- We do **not** host, mirror, or republish any cancer dataset; examples *fetch* from official open
  endpoints at runtime and never commit raw data.
- We do **not** use, reference, or teach against controlled-access (dbGaP, EGA, individual-level
  biobank) or any identifiable patient data — categorically out of scope.
- We do **not** produce **patient-facing** material, clinical guidance, or **medical advice**. The
  audience is scientists; the content is methodological.
- We do **not** present biological or clinical *conclusions* from the example analyses as findings;
  examples exist to teach method, and say so.
- We do **not** build a new workflow engine, ELN, or container runtime; we teach existing tools and
  open standards.
- We do **not** auto-publish to any catalog/portal; a human contributes after review.

## Success metrics (outcomes)

Outcome-based and learner-centric. Vanity metrics ("lessons written", "GitHub stars") are explicitly
excluded. Evidence for each metric is recorded in a committed **outcome ledger**
(`outcomes/<event-id>.json`) with a verifiable reference.

| Metric | Baseline | Target (first ~9 months) |
| --- | --- | --- |
| Learners completing the course who **produce a real reproducible artifact** (containerized analysis + code + data/code-availability statement) for their own work | 0 | ≥ 15 learners with a verifiable artifact (repo/DOI) |
| **Competency gain** on the validated pre/post assessment (containers, provenance, versioning) | n/a (baseline captured in M2 pilot) | median normalized gain ≥ 0.4 across the cohort |
| Cohorts **taught** (workshop or embedded in a course) with the curriculum | 0 | ≥ 2 cohorts taught; ≥ 30 learners reached |
| Institutions/cores/programs that **adopt** the curriculum (teach it themselves) | 0 | ≥ 1 confirmed external adopter |
| **Confirmed teaching/adoption partner(s)** secured | 0 | ≥ 1 secured |
| Hands-on exercises that **build & pass CI** (container green, notebook renders) | n/a | 100% of published exercises green in the last scheduled CI run |
| **License/data-governance defects** found in review (non-open or identifiable data reaching an example) | n/a | **0** (any occurrence is a release-blocking incident) |

Notes on attribution of outcomes:
- A "reproducible artifact" must be **externally verifiable** — a public repository or archived DOI
  whose container builds and whose analysis re-runs from the recorded inputs. Self-reported "I now
  do this" does not count.
- "Adoption" means a third party teaches or embeds the material (a syllabus reference, a run on
  their calendar, a fork taught to their cohort), evidenced by a link/record — not a download.
- **Competency gain** is the class-median *normalized gain* `g = (post − pre) / (max − pre)` on the
  assessment instrument (`assessment-011`), captured at the start and end of a taught cohort.

## Scope

**In scope**
- A modular curriculum (lessons + exercises + worked examples + assessments + instructor notes)
  covering: (A) why reproducibility matters in cancer research; (B) versioning (git, data/protocol
  versioning, DOIs/archiving); (C) provenance (recording how results were produced; metadata
  standards — ISA, FAIR; RO-Crate; electronic lab notebooks at a conceptual level); (D)
  containers/environments (conda/mamba, Docker, Apptainer/Singularity for HPC); (E) reproducible
  analysis (literate programming with Quarto/R Markdown/Jupyter, seeds, dependency pinning); (F)
  sharing & archiving (Zenodo, GEO/SRA, protocols.io, OSF, data/code-availability statements,
  licensing).
- Runnable, CI-tested container recipes and exercise scaffolds.
- Worked examples on **open cancer data only** (see the licensing gate and dataset catalog).
- Reusable artifacts: reproducibility checklist/rubric, data/code-availability statement template,
  environment recipe templates, glossary.
- Pre/post competency assessments + an authentic-assessment **capstone**.
- Instructor guide + **train-the-trainer** kit; accessibility and i18n-readiness.

**Out of scope**
- The data itself (no hosting, mirroring, redistribution, or transformation of any cancer dataset).
- Any controlled-access or identifiable patient data, and any analysis that would require authorized
  access or IRB approval.
- **Patient-facing** content, clinical decision support, treatment/diagnostic guidance, or **medical
  advice** of any kind. (If a patient-facing reproducibility explainer were ever desired, it would be
  a *separate* project at `riskTier: high` with oncologist + patient-advocate review — explicitly not
  this one.)
- Biological/clinical interpretation of the example analyses presented as findings.
- Building new tools (workflow engines, ELNs, container runtimes); we teach existing ones.
- Non-commercial-licensed databases (e.g. COSMIC, OncoKB) as example data sources — excluded by the
  gate (see Data, licensing & compliance).

## Solution approach & architecture

This is a **content/curriculum project with light, testable software** (container recipes + exercise
harnesses + CI). It is not a data pipeline and never moves or stores cancer data.

**Curriculum structure.** Six modules (A–F above) plus a capstone. Each module is a self-contained
unit sized for a single donated AI session plus review, and instantiates one **module template**:

1. **Learning objectives** — 3–6 Bloom-aligned, measurable objectives (verbs like *configure,
   pin, reproduce, audit*), produced by **backward design**: objectives → assessment → content.
2. **Lesson** — short, plain-language narrative for non-computational scientists; every factual
   assertion cited (provenance is both the topic and the method).
3. **Hands-on exercise** — a runnable task in a **pinned container**, with a solution and an
   instructor key; built and tested in CI.
4. **Worked example** — a small, methodological demonstration on **one open cancer dataset**
   (fetched at runtime from an official open endpoint), illustrating the module's skill. No
   biological conclusion is presented as a finding.
5. **Checklist / takeaway artifact** — the reusable rubric/template the learner keeps.
6. **Formative assessment** — short questions/exit ticket mapped to the objectives.
7. **Instructor notes** — timing, common misconceptions, setup, and accessibility guidance.

**Authoring & delivery stack.**
- Lessons in **Markdown** using a Carpentries-compatible structure (so the material can be hosted on
  The Carpentries Workbench / a static site) and/or **Quarto** for executable example notebooks.
- **Container recipes** as `Dockerfile` + an **Apptainer/Singularity** definition (HPC is where bench
  scientists actually run), both pinning base images **by digest** and pinning package versions
  (conda/mamba `environment.yml` with explicit versions; lockfiles where supported).
- **Executable examples** as Quarto/Jupyter documents rendered in CI (e.g. via Quarto render /
  papermill) so a broken example fails the build.
- **TypeScript/ESM + pnpm** per Hee-Lee Oss conventions for any repo tooling (link checkers, the catalog
  validator, the outcome-ledger schema check). The teaching examples themselves are in the learners'
  languages (R/Python/shell) because that is what the audience uses.
- No runtime services; everything runs locally, in a container, or in CI.

**CI / "runnable means runnable".** A scheduled CI matrix (a) builds each container from its pinned
base, (b) runs each exercise's check script, (c) renders each executable worked example, and (d)
runs the link checker and the dataset-catalog validator. A failure marks the affected lesson
**stale** and opens a `maintenance` task; published material must be green in the last scheduled run.

**Open-data access protocol (makes "use but never store" enforceable).** Worked examples touch data
only through a constrained protocol the authors and CI must follow:
- **Fetch from official open endpoints at run time** (e.g. GDC open-access API, DepMap downloads,
  GEO/SRA via official tools) — never a committed copy of the data.
- **Aggregate / de-identified / open tier only**, confirmed against the dataset catalog gate before
  the example is written.
- **Small, bounded slices** sufficient to teach the method (a few genes/samples/rows), not bulk
  extracts.
- **No raw data committed** to the repo, CI artifacts, receipts, or logs; examples cache to an
  ephemeral, git-ignored scratch dir.
- **Stop on any identifiability signal** — if a candidate source turns out to expose individual-level
  or potentially identifiable data, the example is halted and the source routed to EXCLUDE.

**Key decisions.**
- **Template-first**: one module template + one container CI harness, so modules are cheap and
  uniform and quality is structural, not per-author.
- **Gate-before-data**: no worked example is authored until its dataset has a committed PASS gate
  artifact (license permits reuse+derivatives; open/aggregate/de-identified; no identifiable data).
- **Pin everything by digest/version**: reproducibility is taught by example, so the curriculum's own
  artifacts are the strictest demonstration of it.
- **Reuse, don't reinvent**: align with and credit The Turing Way, FAIR, Carpentries, and NIH rigor
  guidance rather than duplicating them; we contribute the *cancer-bench-scientist on-ramp*.

## Data, licensing & compliance

**This is the critical section, and it leads with the cancer guardrails (binding).**

**Binding cancer guardrails (non-negotiable, apply to every task):**
1. **Open-access / aggregate / de-identified data ONLY.** Controlled-access repositories (dbGaP,
   EGA), individual-level biobanks, and **any identifiable patient data are categorically out of
   scope.** No task may require authorized access or IRB approval; if it would, it is rejected, not
   escalated.
2. **Per-source license verification is mandatory** before a dataset appears in any example. A source
   is used only if its license is confirmed to **permit reuse and derivative teaching use**, with the
   license id + URL + a captured snapshot recorded.
3. **No medical advice; methodological only.** The curriculum teaches reproducibility methods to
   scientists. It contains no clinical/treatment/diagnostic guidance and presents no example result
   as a biological/clinical finding. Patient-facing content is out of scope (a separate `high`-risk
   project would be required, with oncologist + patient-advocate review).
4. **Provenance on every assertion.** Every factual claim in the lessons — especially the motivating
   reproducibility-crisis statistics — carries a citation; every example dataset records source,
   version, retrieval date, license, and attribution.
5. **Registries/consent:** this project builds **no registry and stores no data**. Any registry-shaped
   example is limited to *schema/governance illustration* using synthetic or aggregate/deceased-only
   public data, consent-first, never a real data store.

**Dataset allow / flag / deny catalog (maintained as `DATASET-CATALOG.md`, gated per entry).** The
catalog biases hard toward unambiguously open, non-identifiable sources. No entry becomes an example
until it passes the per-dataset gate (`datagate-002`).

- **ALLOW (open / aggregate / de-identified; verify license per entry at the gate):**
  - **GDC / TCGA open-access tier** (open, de-identified summary/aggregate; controlled tier excluded).
  - **DepMap** (Cancer Dependency Map) — released **CC-BY 4.0**; cell-line, not patient.
  - **GEO / SRA** public series — **per-series** check (public-domain US-gov metadata; individual
    series' data-use terms verified at the gate; only de-identified/aggregate series used).
  - **cBioPortal** aggregate/public study views — per-study terms verified.
  - **ICGC open tier**, **Cellosaurus**, **Ensembl**, **gnomAD** (aggregate allele frequencies) —
    per-entry license check.
  - **Synthetic / simulated** data — always allowed and preferred where a real dataset is unnecessary.
- **FLAG / EXCLUDE from examples (non-commercial or registration-gated terms):**
  - **COSMIC** and **OncoKB** — **non-commercial** licensing; **excluded** as example data sources
    (may be *referenced* in prose with attribution, never used as derivative example data).
- **DENY (categorically, never in scope):**
  - **dbGaP, EGA**, any **controlled-access** or **individual-level / identifiable** patient data;
    any source requiring authorized access or IRB.

**Objective "permits derivatives" criterion.** A dataset PASSes only if its license is on the ALLOW
list (or independently verified equivalent) **and** an explicit `license.permitsDerivatives: true`
is recorded with a cited clause/URL, **and** an `identifiability: none|aggregate|deidentified`
field is recorded as non-identifiable. Missing evidence, non-commercial terms, controlled access, or
any identifiability signal = FLAG/EXCLUDE — never default-allow.

**Provenance model.** Every example dataset records: source name + URL, publisher, retrieval
timestamp, version/release, access tier, license id + URL + a captured snapshot (committed copy +
SHA-256 + Wayback save URL), identifiability classification, and the required attribution string.
Every lesson assertion carries an inline citation; a per-module `references.bib`/citation list is
part of the deliverable.

**Privacy/PII stance.** The project **stores no data and processes no individual-level data.** The
dominant privacy concern is upstream — an example accidentally pulling identifiable data — handled by
the DENY rules and the access protocol (open endpoints, bounded slices, stop-on-signal, no committed
data). We never de-identify or anonymize data ourselves (that would be transforming data, out of
scope).

**Attribution & output licensing.** Examples attribute each data source per its license and link the
original. The **instructional content is CC-BY-4.0**; **code and container recipes are MIT**. Where a
source license requires share-alike or specific attribution wording, that wording is reproduced in
the example's data section.

## Quality, review & risk gates

**Risk tier: low** (no patient data, no patient-facing content, no medical advice). Individual tasks
that **touch a real open cancer dataset** are raised to `riskTier: medium` to force domain + data
review. **No task is `high`** — patient-facing content is out of scope, so the high-stakes review
path does not apply here (and if it ever did, the work would be rejected from this project).

**Required review before a deed is "done":**
- **Data & licensing reviewer** (mandatory for any task touching a dataset; the hard gate): confirms
  the source is open/aggregate/de-identified, the license permits reuse+derivatives, no identifiable
  data, and the gate artifact is committed. **Blocking and non-skippable.**
- **Domain reviewer** (cancer bioinformatics): confirms worked examples are technically correct and
  that no biological/clinical claim is presented as a finding or could read as advice.
- **Educator reviewer**: confirms learning objectives are measurable and aligned (backward design),
  assessments match objectives, accessibility met, and the cognitive load suits non-computational
  learners.
- **Technical reviewer**: confirms containers build, exercises pass, examples render — **CI green** —
  and licensing of code (MIT) / content (CC-BY-4.0) is correct.

**Test fixtures & CI (so "CI green" means something).**
- **Container build + smoke test** for every recipe (Docker and Apptainer), base images pinned by
  digest; scheduled rebuilds detect upstream drift.
- **Exercise check scripts** with golden expected outputs; **executable examples render** in CI.
- **Dataset-catalog validator** asserts every example references only a catalog entry with a PASS
  gate artifact and `permitsDerivatives: true` + non-identifiable classification.
- **Link + citation checker** asserts no dead links and that flagged assertions carry citations.

**Definition of Shipped.** A module/curriculum unit is *shipped* when: (1) it passes all four
reviews; (2) its containers/exercises/examples are **green in the last scheduled CI run**; (3) every
example dataset has a committed PASS gate artifact; (4) it is **taught to or adopted by real
learners** (a run delivered, or a named partner teaches/embeds it) with the outcome recorded in the
ledger. Producing the lesson is **not** shipped; learners using it — and, for the project as a whole,
**learners producing reproducible artifacts** — is.

## Roadmap & milestones

**M0 — Foundation & cold-start (thin)**
- Goal: stand up the template + CI + the binding data gate, recruit blocking reviewers, and prove the
  whole flow on **one** pilot module end-to-end; begin partner/cohort outreach.
- **Cold-start de-risking.** The pilot module is the **Containers & environments** module because it
  is the highest-leverage, most self-contained skill and exercises the container-CI harness that all
  later modules depend on. Its single worked example uses the lowest-risk allowed source (DepMap
  CC-BY 4.0, or fully synthetic data) so a real, low-risk end-to-end pass is reachable without waiting
  on a partner.
- Exit criteria: (1) module template + style/accessibility guide published; (2) container CI harness
  builds+tests a recipe (Docker + Apptainer) on a schedule, with the dataset-catalog + link checkers
  wired in; (3) the **open-cancer-data & licensing gate** + initial `DATASET-CATALOG.md` exist and
  are applied to the pilot's dataset (committed PASS artifact); (4) the **pilot module** is complete,
  green in CI, and reviewed by all required reviewers; (5) Data & licensing reviewer, domain
  reviewer, and educator reviewer are **named** (blocking roles filled before pilot review); (6) ≥ 1
  partner/cohort-outreach thread opened.

**M1 — Core skill modules**
- Goal: build the core skills out — **versioning**, **provenance**, **reproducible analysis** — to
  the same bar, and produce the assessment instrument.
- Exit criteria: (1) versioning, provenance, and reproducible-analysis modules published, each green
  in CI with at least one gated worked example or synthetic exercise; (2) the **pre/post competency
  assessment** instrument drafted and reviewed for construct validity by the educator reviewer; (3)
  reproducibility checklist + data/code-availability statement template published; (4) accessibility
  pass (WCAG 2.2 AA) on all published modules.

**M2 — Worked examples, capstone & first taught cohort**
- Goal: deepen worked examples on open cancer data, ship the capstone, and **teach a cohort** to get
  real learner outcomes.
- Exit criteria: (1) sharing/archiving module + capstone published and green; (2) ≥ 3 gated worked
  examples on distinct open cancer datasets across modules (each with a committed PASS gate artifact);
  (3) ≥ 1 cohort **taught**, with pre/post assessment captured (baseline + post) and recorded in the
  outcome ledger; (4) ≥ 1 learner-produced reproducible artifact verified.

**M3 — Scale, train-the-trainer & sustainability**
- Goal: make the curriculum adoptable and maintainable beyond the authors.
- Exit criteria: (1) instructor guide + **train-the-trainer** kit published; (2) ≥ 1 **external
  adopter** confirmed (teaches/embeds the material), recorded with evidence; (3) container/dependency
  **refresh process** documented and a steward identified; (4) ≥ 1 module localized (translation) via
  a domain-qualified reviewer; (5) cumulative outcome targets met (see Success metrics).

Dependencies: M1 depends on the M0 template + CI + gate; M2's examples depend on M1 modules and the
gate; M2's taught cohort depends on the assessment instrument; M3 depends on a body of taught,
reviewed material and at least one delivered cohort.

## Work breakdown

The itemized, schema-mapped backlog lives in `TASKS.md`, organized by the milestones above. Each
milestone has a task table (`ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer`),
acceptance criteria for the most important tasks, and a Definition of Done. A sized-but-unscheduled
backlog and one complete, schema-valid example Task JSON are included there. The **dataset
allow/flag/deny catalog** that feeds the worked-example tasks lives in `DATASET-CATALOG.md`; every
per-example task is blocked on its own committed gate artifact before authoring begins.

## Governance, roles & stakeholders

- **Maintainer (Owner):** TBD — owns the template, CI harness, catalog, and backlog.
- **Data & licensing reviewer:** TBD (name TO BE SECURED) — **mandatory, non-skippable** gatekeeper
  for any dataset use; can read open-data/genomics licenses and apply the open/aggregate/de-identified
  + permits-derivatives + identifiability criteria. Must be filled **before the M0 pilot is reviewed**
  (blocking prerequisite, not a parallel hire). May rotate among ≥ 2 qualified reviewers, but at least
  one must always exist or all dataset work halts. Until named, dataset-touching tasks stay
  `verifiedNeed: false` and no example can pass the gate.
- **Domain reviewer (cancer bioinformatics):** TBD — verifies technical correctness of examples and
  that nothing reads as a biological/clinical finding or as advice.
- **Educator reviewer:** TBD — verifies learning-objective alignment (backward design), assessment
  validity, cognitive load, and accessibility.
- **Technical reviewer(s):** rotation of contributors who verify container builds, exercises, and
  rendered examples (CI green) and code/content licensing.
- **Steward (last-mile owner):** TBD — owns cohort/partner relationships, runs/teaches pilots, and
  records taught-cohort + adoption + learner-artifact outcomes (the "delivered" signal). Critical
  because Definition of Shipped is *taught/adopted*, not *written*.
- **Partner / requestor:** TO BE SECURED — a named training program, core facility, or cohort.

## Dependencies & integrations

- **Pedagogy/standards (credited, not duplicated):** The Carpentries lesson structure + pedagogy;
  Bloom's taxonomy; backward design (Wiggins & McTighe); **The Turing Way**; **FAIR** principles;
  **NIH rigor & reproducibility** guidance; **RO-Crate**, **ISA** metadata model; **CodeMeta**;
  WCAG 2.2 AA.
- **Tooling taught (existing, not built):** git; conda/mamba; Docker; Apptainer/Singularity; Quarto /
  Jupyter / R Markdown; Zenodo; protocols.io; OSF; GEO/SRA submission tooling. Versions referenced in
  exercises are pinned per recipe.
- **Open data sources (per-entry gated):** GDC/TCGA open tier, DepMap (CC-BY 4.0), GEO/SRA public
  series, cBioPortal public studies, ICGC open tier, Ensembl, gnomAD, Cellosaurus, plus synthetic
  data. (COSMIC/OncoKB excluded as example data; dbGaP/EGA/controlled denied.)
- **Hee-Lee Oss pieces:** Task JSON schema (`packages/schema`), the donated-lane CLI workspace/PR flow
  (`packages/cli`), the good-deed definition + refusal guardrails. No funded-lane/runner dependency
  (donated lane).
- **CI:** a scheduled pipeline (container builds, exercise checks, example renders, catalog + link
  validation).

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| A non-open or **identifiable** dataset reaches an example | Low | High | Binding licensing/identifiability gate (`datagate-002`) before authoring; mandatory Data & licensing reviewer; deny-list (dbGaP/EGA/controlled); catalog validator in CI; 0-defect target | Data & licensing reviewer |
| Mis-licensing a source (treating NC/controlled as reusable) | Medium | High | Per-source license verification + committed snapshot; explicit FLAG of COSMIC/OncoKB (NC); `permitsDerivatives` requires cited clause | Data & licensing reviewer |
| **Bit-rot** — exercises/containers stop building | High | Medium | Pin base images by digest + package versions; scheduled CI rebuild; refresh milestone; staleness → `maintenance` task | Maintainer |
| Content drifts into **medical advice** / presents example results as findings | Low | High | Methodological-only scope; domain + educator review; "not advice / teaching example" framing in every example | Domain reviewer |
| No teaching/adoption partner secured → material written but never taught (fails "delivered") | Medium | High | M0 outreach; steward role; self-deliverable pilot workshop fallback; `verifiedNeed:false` until secured | Steward |
| Audience mismatch — material too engineer-centric for bench scientists | Medium | Medium | Backward design; educator review; pilot with real wet-lab learners; cognitive-load guidance in template | Educator reviewer |
| Tool/standard churn (container runtimes, Quarto, RO-Crate spec) | Medium | Low | Pin versions; isolate version bumps to deliberate tasks; credit upstream so we track their releases | Maintainer |
| Accessibility/i18n debt baked in, expensive to retrofit | Medium | Low | WCAG 2.2 AA + i18n-readiness in the template from M0; accessibility task each milestone | Educator reviewer |

## Security & privacy

- **Small threat surface:** no runtime service, no data hosting, no PII processing. Main surfaces are
  CI and the published static material.
- **No data at rest:** worked examples fetch open data at runtime into an ephemeral, git-ignored
  scratch dir and never commit raw data, even aggregate. No individual-level data is ever fetched.
- **Secrets handling:** exercises require no credentials by default. If an open-data endpoint ever
  needs a token (e.g. a courtesy API key), it is supplied by the user at runtime and must never be
  written into logs, receipts, containers, or committed files (per Hee-Lee Oss rules). Container recipes
  embed no secrets.
- **Abuse/misuse prevention:** refuse and flag any task that would (a) steer an example toward
  controlled/identifiable data, (b) launder a non-open dataset as open, (c) re-identify individuals,
  or (d) repurpose the curriculum into clinical/diagnostic guidance. Examples remain methodological
  and source-verified.

## Sustainability & maintenance

- **Post-delivery ownership:** the steward maintains partner/cohort relationships and records
  outcomes; the maintainer keeps the template, CI harness, container recipes, and catalog current.
- **Containers don't rot:** scheduled CI rebuilds plus a periodic **dependency-refresh** task keep
  recipes building; a documented staleness process converts CI failures into `maintenance` tasks.
- **Adoption beyond the authors:** the **train-the-trainer** kit and Carpentries-compatible format let
  other instructors teach it; CC-BY-4.0/MIT licensing permits free reuse and remixing.
- **Outcome tracking:** the steward records taught cohorts, adoptions, and learner-produced
  reproducible artifacts in the outcome ledger against the success metrics, reviewed each milestone.

## Open questions

- Which named training program / core facility / cohort becomes the first confirmed
  teaching/adoption partner?
- Container runtime emphasis for the audience: lead with **Apptainer/Singularity** (HPC reality for
  bench scientists) or **Docker** (easier locally)? (Current default: teach both; examples runnable in
  either.)
- Authoring/hosting platform: **The Carpentries Workbench** vs. **Quarto book** vs. both? (Current
  default: Carpentries-compatible Markdown + Quarto for executable examples.)
- Depth on workflow managers (Nextflow/Snakemake): introduce conceptually in M1 or defer to a backlog
  advanced module? (Current default: conceptual only; advanced module in backlog.)
- For GEO/SRA series, what is the standard per-series license/identifiability check, given series
  vary? (Resolved per entry at the gate; needs a documented sub-checklist.)
- Minimum cohort size and setting (workshop vs. embedded course) for a statistically meaningful
  pre/post competency gain?

## References

- Hee-Lee Oss work rules — `C:\code\hee-lee-oss\CLAUDE.md`
- Good Deed Definition + risk tiers — `C:\code\hee-lee-oss\docs\good-deed-definition.md`
- Task JSON schema — `C:\code\hee-lee-oss\packages\schema\src\schemas.ts`
- Portfolio roadmap (Track 8 cancer guardrails) — `C:\code\hee-lee-oss\planning\ROADMAP.md`
- Dataset allow/flag/deny catalog — `./DATASET-CATALOG.md` (to be created in M0)
- The Turing Way — guide to reproducible, ethical, collaborative data science
- The Carpentries (Software/Data Carpentry) — lesson program & pedagogy
- FAIR Guiding Principles (Wilkinson et al., 2016); RO-Crate; ISA metadata framework; CodeMeta
- NIH Rigor & Reproducibility guidance; Reproducibility Project: Cancer Biology (eLife)
- Bloom's taxonomy (revised, Anderson & Krathwohl); Understanding by Design (Wiggins & McTighe)
- Data sources: GDC/TCGA open tier; DepMap (CC-BY 4.0); GEO/SRA; cBioPortal; ICGC; Ensembl; gnomAD
- WCAG 2.2 AA; Creative Commons CC-BY-4.0; MIT License; SPDX license list

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified during drafting and are **already applied**
in the plan and tasks above.

1. **Binding open-cancer-data & licensing gate** added as an M0 blocking task (`datagate-002`); no
   worked example may be authored before its dataset has a committed PASS gate artifact.
2. **Allow/flag/deny dataset catalog** (`DATASET-CATALOG.md`) specified: ALLOW open/aggregate/
   de-identified (GDC open tier, DepMap, GEO/SRA per-series, etc.); FLAG non-commercial; DENY
   controlled/identifiable.
3. **COSMIC and OncoKB explicitly FLAGGED** as non-commercial and **excluded as example data
   sources** (referenceable in prose only) — a concrete, named licensing trap closed.
4. **dbGaP / EGA / controlled-access / identifiable data categorically DENIED** in scope, not merely
   discouraged — and stated as "rejected, not escalated."
5. **Provenance on every assertion** made a hard rule: lesson claims (incl. reproducibility-crisis
   statistics) cited; a citation/link checker runs in CI.
6. **Container CI harness** (`container-ci-005`) added so "runnable" is *demonstrated* — base images
   pinned **by digest**, scheduled rebuilds, Docker **and** Apptainer.
7. **Outcome metric is behavior change** — learners producing a verifiable reproducible artifact and
   a **normalized pre/post competency gain** — not "lessons written."
8. **Backward design + Bloom-aligned, measurable learning objectives** required for every module via
   the module template (`template-004`).
9. **Carpentries-style pedagogy** (formative assessment, live coding, instructor notes) adopted, with
   a Carpentries-compatible authoring format for downstream adoption.
10. **Accessibility (WCAG 2.2 AA)** — alt text, colorblind-safe figures, plain language — baked into
    the template and given a per-milestone task, not retrofitted.
11. **i18n-readiness in source** so localization (M3 translation) is cheap rather than a rewrite.
12. **Dual licensing stated per deliverable**: CC-BY-4.0 content, MIT code/containers — surfaced in
    scope, tasks, and the example JSON.
13. **Definition of Shipped = taught/adopted**, with learners producing artifacts — not merged —
    matching the Hee-Lee Oss "delivered, not merged" bar.
14. **Steward (last-mile) role** added to own cohort delivery and outcome recording.
15. **Blocking reviewer roles named** (Data & licensing, domain cancer-bioinformatics, educator) and
    required to be filled **before** the M0 pilot is reviewed.
16. **"No medical advice / not for patients" scope boundary** made explicit, with patient-facing work
    routed to a hypothetical *separate* `high`-risk project — so this project carries **no high-risk
    tasks**.
17. **Examples kept methodological** — a standing rule that no biological/clinical conclusion is
    presented as a finding; enforced in domain review.
18. **Container reproducibility across Docker + Apptainer/Singularity** because bench scientists run on
    HPC — a concrete audience-fit decision, not a generic "use Docker."
19. **Dependency-refresh maintenance milestone** (M3) + staleness → `maintenance` task pipeline to
    fight the classic OER death (bit-rot).
20. **Open-data access protocol** (fetch from official endpoints at runtime, bounded slices, no
    committed data, stop-on-signal) makes "use but never store" enforceable.
21. **Reusable durable artifacts** (reproducibility checklist, data/code-availability statement
    template, environment recipe templates) that learners keep — turning a course into tools.
22. **Authentic-assessment capstone** (`capstone-014`): learners make a small open-cancer-data
    analysis fully reproducible and have it checked against the rubric.
23. **CI renders executable examples** (Quarto/papermill) so an example that stops running fails the
    build, not silently misleads learners.
24. **Explicit alignment/credit to The Turing Way, FAIR, Carpentries, NIH rigor** so we interoperate
    and avoid duplicating mature work — our wedge is the *cancer-bench-scientist on-ramp*.
25. **Committed outcome ledger** (`outcomes/<event-id>.json`) requiring externally verifiable evidence
    for every adoption/cohort/artifact claim — no self-reported outcomes count.

---

## Review sign-off

**Completeness check.** All 17 required PLAN sections from `PLAN_SPEC.md` are present and in order
(Executive summary → References), followed by Appendix A and this sign-off. The Data, licensing &
compliance section **leads with the binding cancer guardrails** as instructed. `TASKS.md` provides a
schema-mapped backlog, per-milestone tables, key-task acceptance criteria, milestone Definitions of
Done, a backlog, and a complete schema-valid example Task JSON.

**Correctness fixes applied during review.**
- Confirmed **no `high`-risk tasks** exist, consistent with the "patient-facing = out of scope"
  boundary; dataset-touching tasks set to `medium` to force domain + data review; pure-pedagogy tasks
  `low`.
- Verified the example Task JSON validates against `packages/schema/src/schemas.ts`: all `required`
  fields present; enums correct (`type`, `lane`, `priority`, `riskTier`, `deliverable`,
  `tokenEstimate`, `status`); `acceptanceCriteria` non-empty; `output` non-empty;
  `verifiedNeed: false`; donated lane so no `fundedBudgetUsd` required.
- Ensured **COSMIC/OncoKB (NC)** and **dbGaP/EGA (controlled)** appear in the deny/flag catalog *and*
  in the risk table — the headline licensing/governance gate is consistent across sections.
- Reconciled `verifiedNeed: false` everywhere with the "no partner secured / TO BE SECURED" stance and
  the outcome metric that flips it only on confirmed teaching/adoption.
- Confirmed the M0 pilot is **self-deliverable** (DepMap CC-BY 4.0 / synthetic data, self-run
  workshop fallback) so cold-start does not block on a partner.

**Headline gate.** The release-blocking gate is the **open-cancer-data & licensing/identifiability
gate** (CC-BY/open-tier ALLOW; COSMIC/OncoKB FLAG; dbGaP/EGA/identifiable DENY), enforced by a
mandatory Data & licensing reviewer and a CI catalog validator, with a **0-defect target**.

**Needs a human decision:** (1) secure the first teaching/adoption partner/cohort; (2) name the three
blocking reviewers; (3) choose container-runtime emphasis (Apptainer vs. Docker) and authoring
platform (Carpentries Workbench vs. Quarto). Until (1)–(2) land, all tasks remain
`verifiedNeed: false`.

**Signed off (Draft v0.1.0):** Senior staff engineer + TPM — 2026-06-28. Ready for maintainer review.
