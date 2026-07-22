# reproducibility-curriculum

> Wet-lab and translational cancer scientists routinely produce results that are difficult or impossible for anyone — including their own future selves — to reproduce: analyses run in undocumented, hand  ·  **Risk tier:** low  ·  **Status:** planning

Wet-lab and translational cancer scientists routinely produce results that are difficult or impossible for anyone — including their own future selves — to reproduce: analyses run in undocumented, hand-built software environments; figures whose generating code and inputs are lost; protocols and data tracked in ad-hoc spreadsheets with no version history; and "data/code available on request" statements that resolve to nothing. The cost is borne by patients: a meaningful fraction of preclinical cancer findings do not replicate, slowing the translation of real discoveries into therapies and wasting scarce research funding. The skills that fix this — **versioning, provenance, and computational reproducibility (containers/environments)** — are rarely taught to bench scientists, who are not primarily computational and are poorly served by tutorials written for software engineers.

**Definition of shipped:** reviews; (2) its containers/exercises/examples are **green in the last scheduled CI run**; (3) every example dataset has a committed PASS gate artifact; (4) it is **taught to or adopted by real learners** (a run delivered, or a named partner teaches/embeds it) with the outcome re

This is an **Hee-Lee Oss** good-deed project. Contributors pull a task, do it with their own coding agent, and open a PR. Platform: https://github.com/jdev1977/hee-lee-oss

## Plan
- [PLAN.md](./PLAN.md) — robust enterprise plan (vision, architecture, roadmap, risks; includes an applied-improvements appendix + review sign-off)
- [TASKS.md](./TASKS.md) — schema-mapped task backlog
- [tasks/](./tasks/) — ready-to-pull task JSON(s)

## Contribute
```bash
hee-lee-oss browse
hee-lee-oss next --repo Hee-Lee-Oss-Projects/reproducibility-curriculum --no-fork
```

## Licensing & review
- Open license (see PLAN.md).
- Risk tier **low** — deeds are *delivered, not merged*; standard review applies.

> Planning stage; no adopting partner secured yet (`verifiedNeed: false` on delivery-dependent tasks).
