# Roadmap

This document tracks the evolution of `project-agent-framework`: what is done, what is specified, and what is planned. It is organized as **phases**, where each phase adds a *capability* (or capability maturity) on top of the stable foundation.

The guiding rule: **the foundation and conventions never churn; capabilities layer on.** New phases add directories under `capabilities/` and `templates/` without restructuring existing projects.

---

## Status legend

| Mark | Meaning |
|------|---------|
| ✅ | Done — shipped in this repo |
| 🟦 | Specified — architecture and workflow defined, ready for agents to execute |
| 🛠 | In design — being specified |
| ⬜ | Planned — on the roadmap, not yet specified |

---

## Phase 0 — Foundation ✅

**Goal:** Establish the reusable framework skeleton — conventions, templates, docs, multi-project structure, and the agent contract.

| Item | Status |
|------|--------|
| Four-layer model (Source / Knowledge / Memory / Capabilities) | ✅ |
| Repository structure & uniform project anatomy | ✅ |
| `docs/concepts.md`, `docs/architecture.md` | ✅ |
| `templates/` (source, knowledge, memory, outputs) | ✅ |
| Multi-project isolation under `projects/` | ✅ |
| `sample-project/` reference implementation | ✅ |
| `AGENTS.md` universal agent contract | ✅ |

**Outcome:** Any LLM agent can orient itself and safely read/write a project, even before any capability beyond Meeting Intelligence is specified.

---

## Phase 1 — Meeting Intelligence 🟦

**Goal:** Turn raw meeting transcripts into structured MOMs and reconciled memory. This is the framework's first and currently specified capability.

**Family of sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Project Onboarding | 🟦 | Bootstrap a new project's `project.md`, Knowledge, and Memory from the first batch of source documents. |
| Meeting Analysis | 🟦 | Read a transcript and produce a structured understanding (attendees, agenda, discussion, outcomes). |
| MOM Generation | 🟦 | Write a Minutes of Meeting to `outputs/meetings/*-mom.md`. |
| Requirement Extraction | 🟦 | Source → `memory/requirements.md` (`REQ-###`), reconciled against existing requirements. |
| Decision Extraction | 🟦 | Source → `memory/decisions.md` (`DEC-###`), with supersede links. |
| Action Item Extraction | 🟦 | Source → `memory/action-items.md` (`ACT-###`), with owners and due dates. |
| Open Question Extraction | 🟦 | Source → `memory/open-questions.md` (`Q-###`), to be resolved later. |

**Inputs:** `source/meetings/*` (+ existing `knowledge/`, `memory/` for reconciliation).
**Outputs:** `outputs/meetings/*-mom.md` + updates to `memory/*` (+ `knowledge/*` during onboarding).

**Definition of done for Phase 1:**
- All seven sub-workflows specified as executable Markdown procedures. ✅
- MOM + extraction templates in `templates/outputs/`. ✅
- `sample-project/` demonstrates one full meeting run end-to-end. ✅

See `capabilities/meeting-intelligence/README.md`.

---

## Phase 2 — Requirements Management 🟦

**Goal:** Treat requirements as first-class, traceable, governed artifacts — not just lines extracted from a meeting. Matures the `REQ-###` produced by Meeting Intelligence into clear, classified, traced requirements.

**Specified sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Requirement Refinement | 🟦 | Turn raw `REQ-###` into well-formed requirements (statement, acceptance, priority, rationale, assumptions); promote to `accepted`. |
| Requirement Categorization | 🟦 | Set type (functional/non-functional/constraint), tags, and phase mapping. |
| Traceability | 🟦 | Link requirements ↔ Knowledge (features/modules/actors) and ↔ Source; build a trace matrix. |
| Drift Detection | 🟦 | Flag requirements that conflict with decisions/newer sources, or have gone stale/duplicate/orphan. |
| Coverage Analysis | 🟦 | Report which Knowledge features lack requirements, and vice-versa; phase coverage. |

**Inputs:** `REQ-###` (from Meeting Intelligence) + `knowledge/*`.
**Outputs:** refined `memory/requirements.md`, `memory/assumptions.md` (`ASM-###`), and reports `outputs/reports/requirements-traceability-<date>.md`, `requirements-coverage-<date>.md`, `requirements-drift-<date>.md`.

**Definition of done for Phase 2:**
- All five sub-workflows specified as executable Markdown procedures. ✅
- New templates: `memory/assumptions.md`, `outputs/requirements-traceability.md`, `outputs/requirements-coverage.md`. ✅
- `ASM-###` convention added to `AGENTS.md`. ✅

See `capabilities/requirements-management/README.md`.

---

## Phase 3 — Backlog Management 🟦

**Goal:** Convert agreed requirements and action items into a groomed, prioritized backlog. Closes the loop from Meeting Intelligence — turns accepted requirements into actionable, estimated, dependency-linked work.

**Specified sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Backlog Generation | 🟦 | Derive `BKL-###` backlog items from accepted `REQ-###` and recurring `ACT-###`. |
| Prioritization | 🟦 | Apply a method (e.g., MoSCoW, value/effort) and record rationale as decisions. |
| Estimation Capture | 🟦 | Record size estimates and confidence; surface unknowns as open questions. |
| Dependency Mapping | 🟦 | Link backlog items that block each other; surface the critical path. |
| Grooming / Refinement | 🟦 | Re-evaluate stale items; split large items; close delivered ones. |

**Inputs:** accepted `REQ-###` + recurring `ACT-###` + `knowledge/*`.
**Outputs:** `memory/backlog.md` (`BKL-###`), plus prioritization `DEC-###` and estimation `Q-###`.

**Definition of done for Phase 3:**
- All five sub-workflows specified as executable Markdown procedures. ✅
- Integrates with Meeting Intelligence output (accepted requirements) as input. ✅
- `memory/backlog.md` template in place. ✅

See `capabilities/backlog-management/README.md`.

---

## Phase 4 — Sprint Planning 🟦

**Goal:** Turn the prioritized, estimated backlog into committed, time-boxed sprints — and prepare their review. Consumes ready `BKL-###` from Backlog Management.

**Specified sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Capacity Modeling | 🟦 | Compute team capacity for a sprint window (people, holidays, absences, focus factor, velocity). |
| Sprint Proposal | 🟦 | Recommend a sprint set from `BKL-###` respecting priority, dependencies, and capacity (propose, don't commit). |
| Sprint Commitment | 🟦 | On human approval, finalize scope + owners; reflect into backlog (`status: in-progress`). |
| Sprint Review Prep | 🟦 | At sprint end: completed vs planned, carry-overs, actual velocity, emergent risks/decisions. |

**Inputs:** `BKL-###` (ready) + `knowledge/actors.md` + sprint window.
**Outputs:** `outputs/sprints/sprint-<n>-<date>.md` (lifecycle: proposed → committed → closed); backlog item transitions.

**Definition of done for Phase 4:**
- All four sub-workflows specified as executable Markdown procedures. ✅
- Sprint artifact template: `templates/outputs/sprint.md`. ✅
- Human-in-the-loop on commitment (propose → approve → commit). ✅

See `capabilities/sprint-planning/README.md`.

---

## Phase 5 — Reporting 🟦

**Goal:** Synthesize Knowledge + Memory + Outputs into stakeholder-facing reports on demand. Read-only — produces no new primary data.

**Specified sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Status Report | 🟦 | Weekly/biweekly project status (progress, risks, decisions, blockers). |
| Decision Log Report | 🟦 | Render the decision history with rationale and supersession. |
| Risk Report | 🟦 | Current risk register ranked by exposure, with mitigation status. |
| Open Questions Report | 🟦 | Aging analysis of unresolved questions; highlight blockers + stale. |
| Portfolio Report | 🟦 | Cross-project roll-up from each project's manifest (the first *intentional* cross-project, read-only capability). |

**Inputs:** `memory/*` + `outputs/*` + `knowledge/*` (per project); every `projects/<slug>/project.md` (portfolio).
**Outputs:** `outputs/reports/<topic>-<date>.md` (per project); `reports/portfolio-<date>.md` (repo root, cross-project).

**Definition of done for Phase 5:**
- All five reports specified as executable procedures. ✅
- Five report templates in `templates/outputs/`. ✅
- Portfolio defined as the sanctioned cross-project, read-only exception. ✅

See `capabilities/reporting/README.md`.

---

## Phase 6a — Portfolio Planning 🟦

**Goal:** Add a layer *above* the project so one team can plan sprints that span multiple `projects/<slug>/`. The planning counterpart to Phase 5's read-only portfolio reports.

**Specified sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Portfolio Capacity Modeling | 🟦 | Pooled capacity across in-scope projects' contributors. |
| Portfolio Sprint Proposal | 🟦 | Recommend a cross-project set (`<slug>:BKL-###`) within pooled capacity. |
| Portfolio Sprint Commitment | 🟦 | On human approval, write back `sprint: PS-NN` + `owner:` to each project's backlog (the `AGENTS.md` §7 carve-out). |
| Portfolio Sprint Review Prep | 🟦 | Per-project done/partial, carry-overs, actual velocity. |

**Inputs:** each in-scope project's `memory/backlog.md` (`ready` `BKL-###`) + `knowledge/actors.md`.
**Outputs:** `portfolio/sprints/sprint-<PS-NN>-<date>.md` (repo root); backlog `sprint:`/`owner:` write-back per project.

**Definition of done for Phase 6a:**
- All four sub-workflows specified as executable Markdown procedures. ✅
- New template `templates/outputs/portfolio-sprint.md`. ✅
- New prefixes `PS-NN` + qualified `<slug>:BKL-###` in `AGENTS.md` §3; write-back carve-out in §7. ✅
- `portfolio/` layer + `sample-portfolio/` reference. ✅

> Team profiles power **Phase 6b** (below): skill-based assignment, capability measurement, and effective sprints.

See [`capabilities/portfolio-sprint-planning/README.md`](../capabilities/portfolio-sprint-planning/README.md).

---

## Phase 6b — Team Profiles & Skill-Based Assignment 🟦

**Goal:** Model the build team (the people who *execute* work) so portfolio sprints can assign by skill, measure capability, and plan effective sprints.

**Specified sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Profile Onboarding | 🟦 | Add a `PERSON-###` from an HR/hiring source (reconcile before add). |
| Profile Maintenance | 🟦 | Update skills/level/availability; supersede (`alumni`), never delete. |
| Load Reconciliation | 🟦 | Recompute `current_load` per PERSON from in-flight committed sprints. |
| Skill Assignment & Coverage | 🟦 | Recommend `PERSON-###` owners by skill-overlap + residual capacity; render a coverage matrix; raise `Q-###` for gaps. |

**Inputs:** `portfolio/profiles/team.md` (`PERSON-###`); each BKL's optional `skills_required:`.
**Outputs:** maintained roster; per-person `current_load`; sprint coverage matrix + skill-gap `Q-###`.

**Definition of done for Phase 6b:**
- All four sub-workflows specified. ✅
- Profile template `templates/portfolio/team.md`; `PERSON-###`/`TEAM-###` in `AGENTS.md` §3. ✅
- `BKL.skills_required:` (optional) in the backlog template. ✅
- `sample-portfolio/profiles/team.md` demonstrates coverage + a gap. ✅

See [`capabilities/profile-management/README.md`](../capabilities/profile-management/README.md) and [`capabilities/portfolio-sprint-planning/skill-assignment.md`](../capabilities/portfolio-sprint-planning/skill-assignment.md).

---

## Phase 6 — Cross-cutting & Integration ⬜

**Goal:** Strengthen the framework's portability and connect it to the wider toolchain — *without* compromising the Markdown-first core.

| Item | Status | Note |
|------|--------|------|
| Shared org glossary (`projects/_shared/glossary.md`) | ⬜ | Organization-wide terms referenced by all projects. |
| Bi-directional sync adapters (e.g., Jira, Confluence, Notion) | ⬜ | Treat Markdown as source of truth; sync derived copies. **Optional, opt-in per project.** |
| Validation tooling (lint frontmatter, check ID integrity, broken links) | ⬜ | Plain scripts that *check* files, never replace them as the store of truth. |
| Quality gates for capability runs (completeness checks) | ⬜ | A "completeness critic" step after extraction. |
| Multi-language / localization of templates | ⬜ | Templates translated; conventions unchanged. |

> **Boundary:** Even in Phase 6, the framework remains Markdown-first. Any database, vector store, or API is *built on top of* these files, never *instead of* them. Agents and humans can always fall back to reading the Markdown directly.

---

## Sequencing principles

1. **Foundation before features.** Phase 0 must be stable before capabilities depend on it.
2. **One capability at a time, fully specified.** A 🟦 capability is executable by any agent today; a ⬜ one is a commitment, not a promise.
3. **Memory before planning.** Requirements Management (Phase 2) and Backlog Management (Phase 3) precede Sprint Planning (Phase 4) — you cannot plan what you have not captured.
4. **Reports last, from existing data.** Reporting (Phase 5) only synthesizes what earlier phases produced; it adds no new primary data.
5. **Conventions are forever; capabilities evolve.** The ID conventions, layer disciplines, and `AGENTS.md` rules are stable. Capabilities and templates can change without them.

---

## How to propose a change to this roadmap

Because this is a Markdown repo, proposing a change is a pull request: edit this file, add the capability under `capabilities/` with at least a `README.md`, and add any templates it needs. The architecture in [`architecture.md`](architecture.md) is designed so that new phases slot in without restructuring earlier ones.
