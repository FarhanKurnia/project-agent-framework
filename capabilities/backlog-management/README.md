# Capability — Backlog Management

> **Status:** 🟦 Specified — ready for any LLM agent to execute.
> Phase 3 capability of `project-agent-framework`. Closes the loop from Meeting Intelligence: it turns agreed requirements and recurring action items into a **groomed, prioritized, estimated backlog**.

## Purpose

Convert accepted `REQ-###` (and recurring `ACT-###`) into formal `BKL-###` backlog items — each prioritized, sized, dependency-linked, and traceable back to its origin. This is what makes the project's work *actionable* rather than just *recorded*.

Meeting Intelligence captures **what** was decided and requested; Backlog Management turns that into **what to build, in what order, and how big**.

## Relationship to other capabilities

```
 Meeting Intelligence                  Backlog Management
 ─────────────────────                 ───────────────────
 source/meetings/*  ──▶  REQ-###  ──▶  1. Generation ──▶ BKL-###
                        DEC-###          2. Prioritization (→ DEC-###)
                        ACT-###  ──▶     3. Estimation (unknowns → Q-###)
                                        4. Dependency mapping
                                        5. Grooming (ongoing)
                                              │
                                              ▼
                                         (feeds future Sprint Planning — Phase 4)
```

Backlog items are the **bridge** between Memory (requirements/decisions) and delivery (future Sprint Planning).

## The pipeline

Run steps 1–4 once to stand up a backlog; run step 5 (grooming) **recurringly**.

```
   accepted REQ-### ─┐                    ┌─ 1. Backlog Generation   → BKL-### (new)
                     ├──▶ derive ─────────┤
   recurring ACT-### ┘                    ├─ 2. Prioritization        → priority + DEC-### (rationale)
                                         ├─ 3. Estimation Capture    → size, confidence; unknowns → Q-###
                                         ├─ 4. Dependency Mapping     → blocks / blocked-by links
                                         └─ 5. Grooming (recurring)   → split, close, re-evaluate
```

## Inputs & outputs at a glance

| Step | Reads | Writes |
|------|-------|--------|
| 1. Backlog Generation | `memory/requirements.md` (accepted), `memory/action-items.md`, `knowledge/features.md`, `memory/backlog.md` | `memory/backlog.md` (`BKL-###`) |
| 2. Prioritization | `memory/backlog.md`, `memory/decisions.md` | `memory/backlog.md` (priority), `memory/decisions.md` (`DEC-###` rationale) |
| 3. Estimation Capture | `memory/backlog.md`, `knowledge/*` | `memory/backlog.md` (size, confidence), `memory/open-questions.md` (`Q-###`) |
| 4. Dependency Mapping | `memory/backlog.md`, `memory/requirements.md`, `knowledge/modules.md` | `memory/backlog.md` (`dependencies`) |
| 5. Grooming | `memory/backlog.md`, `memory/requirements.md`, recent `outputs/*` | `memory/backlog.md` (status, splits, closures) |

## Cross-cutting rules (apply to every step)

1. **Provenance is mandatory.** Every `BKL-###` cites its origin via `derived_from: [REQ-### / ACT-###]` and a `source:`.
2. **Reconcile before you write.** Before creating a backlog item, check whether one already exists for the same requirement. Update rather than duplicate.
3. **Respect the ID counter.** `memory/backlog.md` tracks `counter`. Increment per new item; never reuse.
4. **Link liberally.** Each item traces to its `derived_from` (origin) and `delivers` (feature); prioritization records a `DEC-###`; dependencies use `blocks`/`blocked-by`.
5. **Never invent work.** A backlog item must trace to an **accepted** requirement or a committed action item. Unaccepted proposals stay out of the backlog (they are `REQ-###` still at `status: proposed`).
6. **Never delete — close.** Delivered/dropped items get `status: done | dropped` with a note, and remain for history.
7. **One project only.** Confine all writes to the target project. See `AGENTS.md` §7.
8. **Follow `AGENTS.md`.** ID conventions, frontmatter shapes, and editing disciplines are defined there and in `templates/`.

## Step specifications

1. [`backlog-generation.md`](backlog-generation.md)
2. [`prioritization.md`](prioritization.md)
3. [`estimation-capture.md`](estimation-capture.md)
4. [`dependency-mapping.md`](dependency-mapping.md)
5. [`grooming.md`](grooming.md)

## How an agent runs this

> *"Generate and prioritize the backlog for `projects/hris`."*

1. Read `AGENTS.md`, this `README.md`, and the project's `memory/requirements.md`, `memory/action-items.md`, `knowledge/*`, `memory/backlog.md`.
2. Run **Backlog Generation** (step 1) → create `BKL-###` for each accepted requirement / recurring action.
3. Run **Prioritization** (step 2) → assign priority, record rationale as `DEC-###`.
4. Run **Estimation Capture** (step 3) → size + confidence; raise `Q-###` for unknowns.
5. Run **Dependency Mapping** (step 4) → link blocking relationships.
6. Report: items created, priorities set, estimates, dependencies, and open questions raised.
7. (Ongoing) Run **Grooming** (step 5) as requirements evolve or items are delivered.

## Definition of done

- [x] All five steps specified as executable procedures.
- [x] Backlog template (`templates/memory/backlog.md`) already in place.
- [x] Integrates with Meeting Intelligence output (accepted `REQ-###`) as input.
