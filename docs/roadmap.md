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

## Phase 2 — Requirements Management ⬜

**Goal:** Treat requirements as first-class, traceable artifacts — not just extracted lines.

**Proposed sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Requirement Refinement | ⬜ | Turn raw `REQ-###` into well-formed requirements (clear acceptance criteria, priority, rationale). |
| Traceability | ⬜ | Link requirements ↔ Knowledge (modules/features/actors) and ↔ Source. Build a trace matrix. |
| Drift Detection | ⬜ | Flag requirements that conflict with decisions or newer sources, or that have gone stale. |
| Requirement Categorization | ⬜ | Group/tag requirements (functional, non-functional, constraint) and map to scope phases. |
| Coverage Analysis | ⬜ | Report which Knowledge features lack requirements, and vice-versa. |

**New artifacts likely:** `outputs/reports/requirements-traceability-<date>.md`, possibly `memory/assumptions.md` (`ASM-###`).

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

## Phase 4 — Sprint Planning ⬜

**Goal:** Propose sprints from the backlog, capacity, and active decisions.

**Proposed sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Capacity Modeling | ⬜ | Capture team capacity and holidays for a sprint window. |
| Sprint Proposal | ⬜ | Recommend a sprint set from `BKL-###` respecting priority, dependencies, and capacity. |
| Sprint Commitment | ⬜ | Record the committed sprint (scope, owners) — likely in `outputs/sprints/`. |
| Sprint Review Prep | ⬜ | Summarize completed vs. planned, carry-overs, and new risks. |

**New artifacts likely:** `outputs/sprints/sprint-<n>-<date>.md`.

---

## Phase 5 — Reporting ⬜

**Goal:** Synthesize Knowledge + Memory into stakeholder-facing reports on demand.

**Proposed sub-workflows:**

| Sub-workflow | Status | What it does |
|--------------|--------|--------------|
| Status Report | ⬜ | Weekly/biweekly project status (progress, risks, decisions, blockers). |
| Decision Log Report | ⬜ | Render the decision history with rationale and supersession. |
| Risk Report | ⬜ | Current risk register with mitigation status. |
| Open Questions Report | ⬜ | Aging analysis of unresolved questions. |
| Portfolio Report | ⬜ | Cross-project roll-up from each project's manifest (the first *intentional* cross-project capability). |

**New artifacts likely:** `outputs/reports/<topic>-<date>.md`.

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
