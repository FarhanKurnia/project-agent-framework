# Capability — Sprint Planning

> **Status:** 🟦 Specified — ready for any LLM agent to execute.
> Phase 4 capability of `project-agent-framework`. Turns the prioritized, estimated, dependency-linked backlog (Phase 3) into **committed, time-boxed sprints** — and prepares their review.

## Purpose

Given a groomed backlog (`BKL-###`) and a team's capacity, propose a sprint that respects priority, dependencies, and capacity; record the committed scope; and prepare the sprint review. This is where the framework's accumulated Memory becomes **a plan**.

## Relationship to other capabilities

```
 Backlog Management (P3)                    Sprint Planning (P4)
 ─────────────────────                      ─────────────────────
 BKL-### (ready: sized, prioritized,   ──▶  1. Capacity Modeling  → team budget for the window
         dependency-linked)                 2. Sprint Proposal      → proposed set (priority+deps+capacity)
                                            3. Sprint Commitment     → committed scope → outputs/sprints/
                                            4. Sprint Review Prep    → completed vs planned, carry-overs
                                                       │
                                                       ▼
                                            (feeds next Sprint Proposal + Reporting P5)
```

It **consumes** the ready backlog from Backlog Management and **feeds** Reporting (Phase 5) with sprint outcomes.

## The pipeline

Steps 1–3 run at **sprint start**; step 4 runs at **sprint end**.

```
   sprint window (start/end) + team ─┐
                                     ├─ 1. Capacity Modeling   → capacity budget (minus holidays/absences)
   backlog BKL-### (ready) ──────────┤
                                     ├─ 2. Sprint Proposal      → recommended set; carry-forward candidates
                                     ├─ 3. Sprint Commitment    → finalize scope + owners; BKL.status → in-progress
                                     │
   (sprint end)                      └─ 4. Sprint Review Prep   → done vs planned; carry-overs; new RSK/DEC/Q
```

## Inputs & outputs at a glance

| Step | Reads | Writes |
|------|-------|--------|
| 1. Capacity Modeling | `knowledge/actors.md`, sprint window, holidays/absences, prior `outputs/sprints/*` (velocity) | capacity budget (recorded in the sprint artifact) |
| 2. Sprint Proposal | `memory/backlog.md` (`ready` items), capacity from step 1, `memory/decisions.md` | `outputs/sprints/sprint-<n>-<date>.md` (status: proposed) |
| 3. Sprint Commitment | proposed sprint + human approval | `outputs/sprints/sprint-<n>-<date>.md` (status: committed); `memory/backlog.md` (`sprint:`, `status: in-progress`) |
| 4. Sprint Review Prep | committed sprint, `memory/backlog.md` status, recent `outputs/meetings/*`, `memory/risks.md` | sprint artifact review section; `memory/backlog.md` (close done); `memory/risks.md`/`decisions.md`/`open-questions.md` |

## Cross-cutting rules (apply to every step)

1. **Propose, then commit.** The proposal is the agent's recommendation; commitment requires **human approval**. Never auto-commit.
2. **Respect dependencies.** A blocked item (`dependencies:`) cannot be scheduled before its blocker is delivered. The critical path governs sequencing.
3. **Respect capacity.** The proposed set must fit the capacity budget. Overcommitment is a defect, not ambition.
4. **Sprint-readiness gate.** Only `ready` backlog items (sized, `confidence ≥ medium`, per Backlog Management) are eligible. Unsizable/low-confidence items stay out and become carry-forward candidates or `Q-###`.
5. **Provenance & links.** The sprint artifact cites the `BKL-###` it commits; backlog items record the `sprint:` they belong to.
6. **Never delete — transition.** Sprint scope changes by status transitions, not deletion.
7. **One project only.** Confine writes to the target project. See `AGENTS.md` §7.
8. **Follow `AGENTS.md`.** ID conventions, frontmatter, editing disciplines.

## Step specifications

1. [`capacity-modeling.md`](capacity-modeling.md)
2. [`sprint-proposal.md`](sprint-proposal.md)
3. [`sprint-commitment.md`](sprint-commitment.md)
4. [`sprint-review-prep.md`](sprint-review-prep.md)

## How an agent runs this

> *"Propose the next sprint for `projects/hris`, window 2026-07-06 to 2026-07-19."*

1. Read `AGENTS.md`, this `README.md`, and the project's `memory/backlog.md`, `knowledge/actors.md`, prior sprints.
2. Run **Capacity Modeling** (step 1) → compute the team's capacity budget for the window.
3. Run **Sprint Proposal** (step 2) → recommend a set; write `outputs/sprints/sprint-<n>-<date>.md` (status: proposed).
4. **Stop for human approval.** On approval, run **Sprint Commitment** (step 3) → finalize scope/owners, update backlog.
5. At sprint end, run **Sprint Review Prep** (step 4) → record outcomes, carry-overs, new risks.
6. Report at each step: capacity, proposed set + rationale, committed scope, and (at review) completion vs plan.

## Definition of done

- [x] All four steps specified as executable procedures.
- [x] Sprint artifact template: `templates/outputs/sprint.md`.
- [x] Integrates upstream (Backlog Management) and downstream (Reporting).
