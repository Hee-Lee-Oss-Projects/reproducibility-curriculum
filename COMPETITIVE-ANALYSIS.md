# Competitive + Improvement Analysis — `reproducibility-curriculum`

Project: an open, hands-on curriculum teaching reproducibility (versioning, provenance,
containers/environments, data management) to **wet-lab / translational cancer scientists**.
Lane: donated. Risk: low. Guardrails: open/licensed teaching content, accuracy, attribution,
accessibility. Analysis date: 2026-06-29. PLAN.md reviewed: v0.1.0 (2026-06-28).

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually mature for a v0.1 draft: 17 spec sections present, a binding data/licensing
gate, container CI harness, outcome-based (not output-based) metrics, backward-design pedagogy, and
an explicit "delivered = taught/adopted, not written" bar. The following are real findings, ordered
by importance.

**Most important findings**

1. **Audience–content tension is under-operationalized (highest risk to the project's thesis).** The
   plan's entire wedge is "wet-lab / non-computational" learners, yet the in-scope tool list (git,
   conda/mamba, Docker, Apptainer, Quarto/Jupyter/R Markdown, RO-Crate, ISA, lockfiles) is a
   *computational* curriculum. A bench scientist who has never used a terminal cannot reach
   "configure an Apptainer definition" in a single module. The plan names the risk ("too
   engineer-centric") and a mitigation (educator review, pilot) but has **no prerequisite/on-ramp
   model, no command-line/terminal baseline module, and no learner-persona segmentation** (true
   bench-only vs. "lightly analyzes own RNA-seq"). Without an explicit prerequisites map and a
   "module 0: shell & files" on-ramp, the cognitive-load target is aspirational. This is the single
   correctness gap most likely to make the material fail with its stated audience. **Recommend:**
   add learner personas, a prerequisites graph per module, and an explicit decision on whether the
   floor is "never touched a terminal" or "writes basic R/Python scripts" (the latter is what the
   nearest competitor assumes — see §2).

2. **Direct-competitor overlap is acknowledged generically but not specifically — and the nearest
   competitor is omitted.** The plan credits The Turing Way, Carpentries, FAIR, NIH rigor, but does
   **not name the Johns Hopkins / ITCR "Introduction to Reproducibility in Cancer Informatics"**
   course (Coursera + open Bookdown, CC-BY, NCI-funded), which is the closest existing artifact in
   the world: open, hands-on, cancer-domain, reproducibility-focused, R/Python. The differentiation
   strategy ("cancer-bench-scientist on-ramp") is sound but the plan must position *against this
   specific resource*, not just the generic giants, or risk re-building 70% of an existing CC-BY
   course. **Recommend:** add a named "prior-art / do-not-duplicate" register (JHU/ITCR, Carpentries
   Incubator Docker & "Managing Open & Reproducible Computational Projects", NBIS, Turing Way) with
   a per-competitor "what we add" column. See §3–§4.

**Other correctness/completeness notes**

- **Learning objectives & assessment (strong).** Backward design, Bloom verbs, pre/post normalized
  gain `g`, construct-validity review by an educator, authentic capstone — this is best-practice and
  better than most competitors, who rarely measure competency gain. Minor gap: a single assessment
  instrument (`assessment-011`) is planned but **no validated item bank or reliability target**
  (Cronbach's α / item discrimination); "validated" is asserted, not operationalized. n≥? cohort
  size for a meaningful gain is correctly flagged as an open question.
- **FAIR / TOP / Turing Way alignment.** FAIR, RO-Crate, ISA, CodeMeta, NIH rigor are cited
  appropriately. **TOP (Transparency & Openness Promotion) guidelines and the FAIR4RS (FAIR for
  Research Software) principles are not named** — both are standard reference frames a reviewer would
  expect; add them. Turing Way alignment is good but should specify *which* Turing Way chapters are
  upstreamed-to vs. linked (avoid forking their content).
- **Hands-on environment (strong, with a gap).** Pinning base images by digest, Docker + Apptainer,
  scheduled CI rebuild, Quarto/papermill render-in-CI — this is genuinely stronger than competitors,
  most of whom let containers bit-rot. **Gap:** no stated plan for *how a non-technical learner runs
  the exercise* (local Docker Desktop licensing for institutions, no-install options like
  Codespaces / Binder / JupyterHub / GitPod, institutional HPC access). "Runnable in CI" ≠ "runnable
  by a bench scientist on a locked-down lab laptop." This is a delivery blocker worth an explicit
  decision.
- **Currency of tools (mostly current).** conda/**mamba**, **Apptainer** (correct post-Singularity
  name), Quarto, RO-Crate are current as of 2026. **Podman** (now the Carpentries' default container
  engine, and the rootless default on many HPC/institutional setups) is **not mentioned** — add it
  alongside Docker. **Pixi** (the emerging conda-ecosystem lockfile/environment manager) and **`uv`**
  (Python) are worth at least a forward-reference; "conda environment.yml with explicit versions" is
  current but no longer the only best practice. Nextflow/Snakemake correctly deferred to a backlog
  advanced module (good scoping decision).
- **Accessibility (strong on paper).** WCAG 2.2 AA, alt text, colorblind-safe figures, plain
  language, i18n-readiness, per-milestone accessibility task. This exceeds nearly every competitor.
  Verify: code-heavy/terminal content and container output are hard to make AA (contrast in
  screenshots, screen-reader-hostile ASCII) — needs a concrete code-block/terminal accessibility
  pattern, not just a policy.
- **Not duplicating Carpentries/Turing Way (well-handled).** "Reuse, don't reinvent" + Carpentries-
  compatible Workbench format + credit-upstream is the right posture. Strengthen by committing to
  *contribute back* (Carpentries Incubator submission, Turing Way chapter) as a distribution channel.
- **Scope vs. siblings (clean, one ambiguity).** Distinct from **`ewing-reproducibility`** (which
  *does* reproduction of specific computational cancer analyses — a "doing" project, not a course)
  and **`bioinformatics-from-zero`** (teaches *data analysis* skills from scratch). The ambiguity:
  `bioinformatics-from-zero` and this curriculum will both need a "shell + git + environments"
  on-ramp — risk of **duplicated foundational modules**. Recommend a shared-foundations decision
  (one project owns the on-ramp, the other depends on it). Also clarify the boundary with
  `lab-protocols-open` (protocol versioning/provenance is in both) and `onco-research-software-docs`
  (documentation overlaps the "documenting analysis" topic).
- **Risk tiering correct.** Low overall; dataset-touching tasks → medium; no high tasks (patient-
  facing out of scope). Consistent with CLAUDE.md guardrails. The licensing gate (COSMIC/OncoKB
  FLAG-NC, dbGaP/EGA DENY-controlled, `permitsDerivatives` + identifiability evidence required) is
  the standout strength and matches the binding cancer guardrails.

---

## 2. Competitive landscape

| Resource | Strengths | Weaknesses (vs. this project) |
|---|---|---|
| **JHU / ITCR "Introduction to Reproducibility in Cancer Informatics"** — Coursera + open Bookdown, CC-BY, NCI-funded ([coursera](https://www.coursera.org/learn/intro-reproducibility-cancer-informatics), [ITCR network](https://www.itcrtraining.org/)) | Closest existing artifact: open, hands-on, **cancer-domain**, R/Python, 8 modules (notebooks, git/GitHub, package versions, durable code, code review, documentation). Free, no-login Bookdown. | **Assumes prior scripting** (R/Python) — not true wet-lab on-ramp. **Containers/Docker mentioned but not taught deeply; no Apptainer/HPC; thin on data management/provenance/archiving.** No competency-gain measurement, no train-the-trainer, no container CI. **This is the resource to beat — and the gaps are exactly our wedge.** |
| **The Turing Way** — handbook for reproducible/ethical/collaborative research ([book](https://book.the-turing-way.org/reproducible-research/reproducible-research/), [repo](https://github.com/the-turing-way/the-turing-way)) | The dominant open resource. Comprehensive, community-maintained, CC-BY, authoritative, huge reach, covers version control, containers, provenance, RO-Crate, ethics. | **Reference handbook, not a taught course**: no scaffolded objectives, no graded exercises, no runnable container CI, **no domain (cancer) examples, no competency assessment, not pitched to bench scientists.** Breadth over hands-on depth. |
| **The Carpentries** — Software/Data Carpentry + Incubator (Docker/Podman, "Managing Open & Reproducible Computational Projects") ([lessons](https://carpentries.org/lessons/), [Docker lesson](https://carpentries-incubator.github.io/docker-introduction/)) | Gold-standard pedagogy (live coding, formative assessment, instructor training), CC-BY, mature Workbench, large instructor network. Docker/Podman lesson is solid. | **Generic, not cancer/wet-lab**; container lesson is **Podman/Docker laptop-only, explicitly punts Apptainer/HPC to a separate lesson**; lessons not always domain-relevant; bit-rot in Incubator lessons; no cancer data examples. |
| **NASA TOPS — Open Science 101** ([course](https://science.nasa.gov/open-science/tops/os101/)) | Massive scale (goal 20k+ trained), 5 modules, badge/certificate, very accessible, open. Excellent *open-science* framing. | **Open science ≠ computational reproducibility depth**: light on containers/environments/provenance tooling; space/Earth-science framed, **not biomedical/cancer, not wet-lab**; awareness-level, not hands-on container engineering. |
| **Coursera "Reproducible Research" (JHU)** ([course](https://www.coursera.org/learn/reproducible-research/)) | Long-running, popular, teaches literate analysis + R Markdown + reproducible reporting. | R/stats-analyst audience; **no containers, no cancer domain, no provenance/data-governance, dated toward R Markdown only.** |
| **NBIS Reproducible Research course** ([site](https://nbis-reproducible-research.readthedocs.io/)) | Strong, modern, **bioinformatics-tuned**: git, conda, Snakemake/Nextflow, Docker/Singularity, Jupyter/R Markdown. Open. | **Computational/bioinformatics audience, not wet-lab on-ramp; not cancer-specific; no competency assessment, no accessibility/i18n emphasis, no train-the-trainer kit.** Sweden/ELIXIR-centric. |
| **Harvard Online "Principles, Statistical & Computational Tools for Reproducible Data Science"** ([course](https://www.harvardonline.harvard.edu/course/principles-statistical-computational-tools-reproducible-data-science)) | Rigorous, biostatistics/comp-bio framed, git + repos + dynamic reports. | **Paid, not open; biostatistician audience; not wet-lab; light on containers/HPC.** |
| **FOSTER / FORRT Open Science training** ([FOSTER](https://www.fosteropenscience.eu/), [FORRT](https://forrt.org/)) | Broad open-science e-learning, badges, multilingual, 12 self-paced courses incl. "reproducible research practitioner." | **Awareness/policy level, not hands-on tooling; not biomedical; EU-policy framed; little container/provenance practice.** |
| **ELIXIR TeSS / Institut Curie / Physalia / INTERSECT-style HPC training** ([TeSS](https://tess.elixir-europe.org/), [Curie Nextflow](https://training.institut-curie.org/courses/nextflow-for-computational-biology-workflows)) | Real bioinformatics/HPC depth (Nextflow + Apptainer, FAIR), some cancer-genomics framing (IARC pipelines). | **Aimed at bioinformaticians/HPC users — the opposite end of our audience**; pipeline-engineering focus; not a beginner wet-lab curriculum; fragmented, varying quality/maintenance. |

---

## 3. Gaps we can fill

The market is bimodal: **generic-but-shallow** (Turing Way, Carpentries, TOPS, FOSTER) and
**deep-but-for-computational-people** (NBIS, Curie, Physalia). The JHU/ITCR cancer course sits
closest to us but **assumes prior scripting and stops short of containers/HPC/data-governance**. The
unoccupied gap is precisely:

1. **A true wet-lab / non-computational on-ramp** — starts below "you can write a script," uses
   bench-relevant artifacts (a qPCR plate, a flow gate, an imaging batch, an RNA-seq count matrix),
   and treats the terminal/git/containers as new, not assumed.
2. **Deep, *runnable*, bit-rot-resistant containers** for the audience that actually uses **HPC
   (Apptainer)** and locked-down lab laptops — with no-install fallbacks. Competitors either skip
   containers (JHU, Coursera) or punt HPC to a separate lesson (Carpentries).
3. **Cancer-domain worked examples on open data** with a *binding licensing/identifiability gate* —
   no general-purpose course has this governance rigor; bioinformatics courses use whatever data.
4. **Provenance + data/protocol management for bench work** (RO-Crate, ISA, ELN concepts, protocol
   versioning, data/code-availability statements) — thin or absent everywhere for this audience.
5. **Competency measurement (normalized pre/post gain) + authentic capstone** — almost no competitor
   measures behavior change; they measure completion/badges.
6. **Train-the-trainer + Carpentries-compatible format + accessibility (WCAG 2.2 AA) + i18n** — the
   combination is rare; it turns a course into something cores can adopt and localize.
7. **Durable take-home tools** (reproducibility checklist, data/code-availability template,
   environment-recipe templates) — most courses leave learners with knowledge, not reusable assets.

---

## 4. Differentiators to win (incl. vs. The Turing Way)

1. **Audience wedge: the bench-scientist on-ramp.** Everyone else assumes scripting fluency or is
   reference material. Win by being the *only* course that takes a wet-lab postdoc with no terminal
   experience to a containerized, archived, reproducible analysis of their own data.
2. **vs. The Turing Way specifically:** Turing Way is the encyclopedia; we are the **guided,
   assessed, runnable course** that *uses and links into* it. Don't compete on breadth — **depend on
   it, cite it, and contribute cancer-flavored chapters upstream.** Our differentiators it cannot
   match as a handbook: scaffolded objectives, graded hands-on exercises, **container CI that proves
   the exercise still runs**, cancer worked examples, and measured competency gain.
3. **"Runnable means runnable" guarantee.** Scheduled CI that rebuilds every container from pinned
   digests and renders every example — a maintenance commitment competitors structurally lack.
   "Green in the last scheduled run" is a marketing claim no handbook can make.
4. **Governance as a feature, not a footnote.** The binding open-data/licensing/identifiability gate
   is a credibility signal to cancer institutions (IRB-adjacent comfort) that generic courses can't
   offer; it also *teaches by example* (the course practices the data hygiene it preaches).
5. **Outcome bar = taught + learner-produced reproducible artifact**, recorded in a verifiable
   ledger. We sell *behavior change*, not completion certificates.
6. **Adoptability:** Carpentries-compatible + CC-BY/MIT + train-the-trainer + i18n + accessibility =
   a core facility can pick it up and run it next quarter. This is the distribution moat.

---

## 5. Claude API leverage (and hard limits)

**Where Claude is strong (draft-and-verify):**

1. **Lesson/exercise/checklist drafting at scale** — generate first-draft module narratives, Bloom-
   aligned objectives, formative-assessment items, exit tickets, glossary entries, and the
   reproducibility/data-availability checklists from the module template; produce instructor notes
   (timing, common misconceptions). Fastest, highest-leverage use.
2. **Worked examples, container configs & scaffolds** — draft Dockerfiles, Apptainer `.def` files,
   `environment.yml`/lockfile skeletons, Quarto/notebook example scaffolds, and exercise check
   scripts with golden outputs — *then run them in CI to verify* (never ship un-run).
3. **Assessment & analysis support** — generate pre/post item banks mapped to objectives, distractor
   rationales, rubric language for the capstone, and accessibility passes (alt-text drafts,
   plain-language rewrites, reading-level checks), and translation drafts for i18n.
4. (Bonus) **Prior-art/competitor diffing** and **citation-finding drafts** for the
   provenance-on-every-assertion rule — surfacing candidate sources for human verification.

**Where Claude must NOT be the decider (human/CI-gated):**

- **Technical accuracy is verified by *running*, not by the model.** Every container must build and
  every example must execute in CI; Claude's claim that a Dockerfile works is not evidence. No
  "fabricated tooling behavior" (e.g., asserting a flag/command exists) ships unrun.
- **Pedagogy is reviewed by educators.** Objective alignment, cognitive load for non-computational
  learners, and assessment construct validity are human-reviewed (backward-design reviewer), not
  model-judged.
- **Licenses and data governance are human-verified.** The Data & licensing reviewer — not Claude —
  makes the PASS/FLAG/DENY call; `permitsDerivatives`/identifiability evidence is human-confirmed
  with a committed snapshot. Claude may *draft* the gate artifact; it may not *approve* it.
- **Reproducibility-crisis statistics and all factual claims** require a real, human-checked citation
  — no model-generated stats or sources.
- **Cancer domain correctness** (no example reads as a biological/clinical finding or advice) is
  domain-reviewer territory.

---

## 6. Ten concrete optimizations

1. **Add a "Module 0: shell, files & your computer" on-ramp** + per-module **prerequisites graph**
   and **learner personas** (bench-only vs. light-analyst). Resolves the §1 audience gap directly.
2. **Adopt a no-install delivery path** (Binder / GitHub Codespaces / institutional JupyterHub) as a
   first-class option beside local Docker, so locked-down lab laptops aren't a blocker. Decide
   Docker Desktop licensing stance for institutions.
3. **Add Podman** as a taught/option engine (Carpentries default; rootless on HPC/institutional
   machines) and forward-reference **Pixi / `uv`** lockfiles alongside conda `environment.yml`.
4. **Publish a named prior-art register** (JHU/ITCR, Turing Way chapters, Carpentries Incubator,
   NBIS) with a per-resource "reuse vs. add" decision — and commit to **contributing back** (Turing
   Way chapter, Carpentries Incubator submission) as a distribution channel, not just citing.
5. **Map the curriculum to TOP guidelines and FAIR4RS** (in addition to FAIR/NIH rigor) so reviewers
   and adopters see standard alignment; add a one-page crosswalk.
6. **Strengthen the assessment instrument**: define an item bank, reliability target (α / item
   discrimination), and a minimum cohort size for a meaningful normalized-gain claim (close the open
   question). Pilot the instrument before M2 cohort.
7. **Ship a terminal/code-block accessibility pattern** (not just a policy): screen-reader-friendly
   code presentation, no information-in-screenshots-only, captioned/transcribed any demo, high-
   contrast terminal theme — and test with assistive tech.
8. **Bench-relevant worked examples**: anchor each module in an artifact the audience recognizes
   (qPCR plate, flow gate, imaging batch, RNA-seq count matrix from DepMap/GDC open tier) rather
   than abstract data — raises perceived relevance and retention.
9. **Shared-foundations agreement with `bioinformatics-from-zero`**: one project owns the
   shell/git/environments on-ramp; the other depends on it. Prevents duplicated foundational modules
   and a maintenance fork.
10. **Pre-register the data gate as a reusable, machine-checkable schema** (the catalog validator)
    and publish it as a standalone artifact — useful to every sibling cancer-data project and a
    differentiator no competitor offers.

---

## 7. Parallel & perpendicular spin-offs

**Parallel (same lane, reuse the engine):**
- **Reusable "reproducibility-training kit"** — the module template + container CI harness +
  catalog validator + assessment instrument + accessibility checklist, packaged domain-agnostic.
  Any field (not just cancer) can fork it; the cancer curriculum becomes the reference instantiation.
- **`bioinformatics-from-zero` shared on-ramp** — co-own the shell/git/environments foundation;
  this curriculum picks up where it ends (reproducibility practices), avoiding overlap.
- **`onco-research-software-docs`** — the "documenting analysis" module and durable-artifact
  templates feed directly into a documentation-standards effort; cross-link rubrics.

**Perpendicular (different deliverable, shared assets):**
- **`ewing-reproducibility`** — that project *does* reproductions of specific computational analyses;
  this curriculum can supply the *training* its contributors need, and its real reproduction attempts
  become authentic worked examples (case studies) here. Strong two-way tie: course ↔ practice.
- **`lab-protocols-open`** — protocol versioning/provenance is shared ground; co-develop the
  protocol-versioning + data/code-availability templates so wet-lab protocol provenance and
  computational provenance use one mental model.
- **A reproducibility MCP server** — a tool that, given a repo, checks for the taught practices
  (pinned containers, env lockfile present, seeds set, data/code-availability statement, license,
  RO-Crate metadata) and emits a reproducibility-checklist score. Doubles as a teaching aid (learners
  run it on their capstone) and an outcome-verifier (confirms a "reproducible artifact" claim in the
  outcome ledger). Reusable across every sibling project and a genuine differentiator.
- **Outcome-ledger / artifact-verifier service** — generalizes the "externally verifiable
  reproducible artifact" check (container builds, analysis re-runs) into a shared Elyos capability.

---

## 8. Open questions

- **Audience floor:** is the true baseline "never opened a terminal" or "writes basic R/Python"?
  This decision drives whether Module 0 and a no-install path are mandatory. (Plan currently
  ambiguous; the nearest competitor assumes the latter.)
- **Delivery for locked-down lab laptops:** local Docker vs. Codespaces/Binder/HPC JupyterHub —
  which is the supported default, and who pays for hosted compute?
- **Container emphasis:** Apptainer-first (HPC reality) vs. Docker/Podman-first (laptop ease)? (Plan
  default: both — but "both" doubles maintenance; confirm CI can sustain it.)
- **Authoring platform:** Carpentries Workbench vs. Quarto book vs. both (maintenance cost of both).
- **First confirmed teaching/adoption partner** and the three blocking reviewers — still TBD; until
  named, all tasks remain `verifiedNeed: false`.
- **Assessment validity:** item bank, reliability target, and minimum cohort size for a meaningful
  normalized-gain claim.
- **Do-not-duplicate boundary with JHU/ITCR cancer course:** explicitly decide what we *link to* vs.
  *rebuild* (e.g., reuse their git/notebooks framing, add containers/HPC/provenance/data-governance).
- **Shared-foundations ownership** between this curriculum and `bioinformatics-from-zero`.

---

## Summary (for the requester)

The market splits in two: **generic-but-shallow** (The Turing Way, Carpentries, NASA TOPS, FOSTER)
and **deep-but-for-already-computational-people** (NBIS, Institut Curie/ELIXIR, Harvard Online).
The **top three competitors** are: (1) **Johns Hopkins / ITCR "Introduction to Reproducibility in
Cancer Informatics"** — the closest existing artifact (open, CC-BY Bookdown, cancer-domain,
hands-on) but it *assumes prior scripting* and stops short of containers, HPC/Apptainer, and data
governance; (2) **The Turing Way** — the dominant open *reference handbook*, comprehensive but not a
scaffolded, assessed, runnable course; (3) **The Carpentries** — gold-standard pedagogy and a solid
Docker/Podman lesson, but generic (not cancer/wet-lab) and it explicitly punts Apptainer/HPC.

**Single strongest differentiator:** the **true wet-lab / non-computational on-ramp** — the only
course taking a bench scientist with no terminal experience to a containerized, archived,
*CI-proven-runnable* reproducible analysis of their own cancer data, with a binding open-data
licensing gate. No competitor occupies this; against the Turing Way we should *depend on and
contribute to it*, not compete on breadth.

**Top three Claude-API ideas:** (1) draft module narratives, Bloom-aligned objectives,
checklists, assessment items, and instructor notes from the module template; (2) generate
Dockerfiles / Apptainer defs / lockfiles / Quarto example scaffolds and exercise check scripts —
then *verify by running in CI*; (3) build the pre/post item bank, rubric language, and accessibility
+ i18n passes. Hard limits: technical accuracy proven by execution (never un-run), pedagogy
educator-reviewed, licenses/identifiability human-verified, and every reproducibility-crisis stat
human-cited — no fabricated tooling behavior.

**Two most important plan-correctness findings:** (1) the audience→content tension is
under-operationalized — the in-scope tool stack is a *computational* curriculum with **no
prerequisites map, no terminal on-ramp, and no learner-persona segmentation**, which most threatens
the wet-lab thesis; (2) the **nearest competitor (JHU/ITCR) is unnamed** in the plan — the
do-not-duplicate strategy must position against that specific CC-BY cancer course (and the
Carpentries containers/HPC split), not only the generic giants.
