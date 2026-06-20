# Capability — Requirements Management

> **Status:** 🟦 Specified — ready for any LLM agent to execute.
> Phase 2 capability of `project-agent-framework`. Treats requirements as **first-class, traceable, governed artifacts** — not just lines extracted from a meeting.

## Purpose

Meeting Intelligence *captures* requirements (`REQ-###`, often at `status: proposed`). Requirements Management **matures and governs** them: refines raw statements into well-formed requirements, classifies and phase-maps them, traces each to Knowledge and Source, detects drift over time, and reports coverage gaps.

In short: capture asks **"what was said?"**; this capability asks **"is each requirement clear, classified, traceable, consistent, and covered?"**

## Relationship to other capabilities

```
 Meeting Intelligence                      Requirements Management
 ─────────────────────                     ────────────────────────
 source/meetings/* ──▶ REQ-### (proposed) ──▶ 1. Refinement     → well-formed; promote to accepted
                                              2. Categorization  → type, tags, phase
                                              3. Traceability    → REQ↔FEAT↔MOD↔source; matrix
                                              4. Drift Detection → conflicts/stale/dupes/orphans
                                              5. Coverage        → feature↔requirement gaps
                                                     │
                                                     ▼
                                         accepted REQ-###  ──▶  Backlog Management (Phase 3)
```

It **consumes** Meeting Intelligence output and **feeds** Backlog Management (only `accepted`, well-traced requirements should become backlog items).

## The pipeline

Steps 1–2 are run after each intake of new requirements; steps 3–5 are run **recurringly** to keep the requirement set healthy.

```
   proposed/raw REQ-### ─┐
                         ├─ 1. Refinement       → statement, acceptance, priority, rationale → status: accepted
                         ├─ 2. Categorization    → type, tags, phase mapping
                         │
   (recurring)           ├─ 3. Traceability      → REQ↔FEAT↔MOD↔ACTOR↔source  → trace matrix report
                         ├─ 4. Drift Detection    → conflicts / stale / duplicates / orphans
                         └─ 5. Coverage Analysis  → features w/o requirements (and vice-versa)
```

## Inputs & outputs at a glance

| Step | Reads | Writes |
|------|-------|--------|
| 1. Refinement | `memory/requirements.md` (esp. `proposed`), `knowledge/*`, `memory/decisions.md`, `memory/assumptions.md` | `memory/requirements.md`, `memory/assumptions.md`, `memory/open-questions.md` |
| 2. Categorization | `memory/requirements.md`, `knowledge/scope.md` | `memory/requirements.md` (type/tags/phase) |
| 3. Traceability | `memory/requirements.md`, `knowledge/features.md`, `knowledge/modules.md`, `knowledge/actors.md`, `source/*` | `outputs/reports/requirements-traceability-<date>.md`, `memory/requirements.md` (links) |
| 4. Drift Detection | `memory/requirements.md`, `memory/decisions.md`, `source/*` (newer), `memory/risks.md` | `memory/requirements.md` (status/supersede), `memory/open-questions.md`, `outputs/reports/requirements-drift-<date>.md` |
| 5. Coverage Analysis | `memory/requirements.md`, `knowledge/features.md`, `knowledge/scope.md` | `outputs/reports/requirements-coverage-<date>.md`, `memory/open-questions.md` |

## Cross-cutting rules (apply to every step)

1. **Provenance is mandatory.** Requirements keep their `source:`; new assumptions get their own `source:`.
2. **Never fabricate.** Refinement fills gaps only from sources/decisions; anything genuinely missing becomes an `ASM-###` (assumption, explicitly flagged) or a `Q-###`.
3. **Reconcile-first.** Before creating or promoting, check for an existing equivalent requirement.
4. **Traceability is bidirectional.** A requirement links to its feature(s); coverage analysis checks the reverse.
5. **Never delete — supersede.** Drift is resolved by `status: superseded` + `superseded_by`, never deletion.
6. **Status gating.** Only `accepted` requirements (refined + categorized) feed Backlog Management.
7. **One project only.** Confine writes to the target project. See `AGENTS.md` §7.
8. **Follow `AGENTS.md`.** ID conventions (`REQ/ASM/Q`), frontmatter, editing disciplines.

## Step specifications

1. [`requirement-refinement.md`](requirement-refinement.md)
2. [`requirement-categorization.md`](requirement-categorization.md)
3. [`traceability.md`](traceability.md)
4. [`drift-detection.md`](drift-detection.md)
5. [`coverage-analysis.md`](coverage-analysis.md)

## How an agent runs this

> *"Refine and trace the requirements for `projects/hris`."*

1. Read `AGENTS.md`, this `README.md`, and the project's `memory/requirements.md`, `knowledge/*`, `memory/decisions.md`, `memory/assumptions.md`.
2. Run **Refinement** (step 1) → improve each `proposed` requirement; promote clear ones to `accepted`.
3. Run **Categorization** (step 2) → set type/tags/phase.
4. Run **Traceability** (step 3) → ensure links; write the trace matrix report.
5. (Recurring) Run **Drift Detection** (step 4) and **Coverage Analysis** (step 5) → flag issues, write reports.
6. Report: requirements refined/promoted, assumptions raised, trace gaps, drift, and coverage holes.

## Definition of done

- [x] All five steps specified as executable procedures.
- [x] New templates: `memory/assumptions.md` (`ASM-###`), `outputs/requirements-traceability.md`, `outputs/requirements-coverage.md`.
- [x] Integrates upstream (Meeting Intelligence) and downstream (Backlog Management).
