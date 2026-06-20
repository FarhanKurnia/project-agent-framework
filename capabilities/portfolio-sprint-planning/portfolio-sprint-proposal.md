# Step 2 — Portfolio Sprint Proposal

> Part of [Portfolio Sprint Planning](README.md). Produces a **recommendation**, not a commitment. Extends [`../sprint-planning/sprint-proposal.md`](../sprint-planning/sprint-proposal.md).

## Purpose

Recommend a cross-project sprint set from each in-scope project's `ready` backlog — qualified as `<slug>:BKL-###` — that respects priority, dependencies (including cross-project), and the pooled capacity.

## Inputs

- Each in-scope project's `memory/backlog.md` (`ready` items).
- Pooled capacity from step 1.
- `portfolio/manifest.md` (sprint counter → next `PS-NN`).

## Procedure

1. **Collect & qualify:** from each in-scope `memory/backlog.md`, take `ready` items (`size` set, `confidence ≥ medium`). Rewrite each reference as `<slug>:BKL-###`.
2. **Order** across the pool: by `priority`, then dependency (blocker before blocked — honoring cross-project deps), then size.
3. **Select greedily within capacity:** pull in order until cumulative size reaches the budget.
4. **Respect dependencies absolutely:** never include a blocked item whose blocker is not also in-scope (or already delivered). Cross-project deps are written `depends_on: [<slug>:BKL-###]`.
5. **Draft a cross-project sprint goal.**
6. **List carry-forward candidates** (high-priority items that didn't fit) and **exclusions with reasons** (blocked, not ready, low confidence → `Q-###`).
7. **Write** `portfolio/sprints/sprint-<PS-NN>-<date>.md` from the template (status: **proposed**). Increment `sprint_counter` in `manifest.md`.
7b. **Skill assignment & coverage** — run [`skill-assignment.md`](skill-assignment.md): recommend a `PERSON-###` owner per item by skill-overlap + residual capacity, fill the *Owner* + *Skills needed* columns, render the **coverage matrix**, and raise `Q-###` for skill gaps (gap items move to carry-forward). Skip if no roster exists (free-text owners then).
8. **Stop for human approval** before step 3.

## Outputs

| Artifact | Notes |
|----------|-------|
| `portfolio/sprints/sprint-<PS-NN>-<date>.md` | Proposed (status: proposed). |
| `portfolio/manifest.md` | `sprint_counter` incremented. |
| per-project `memory/open-questions.md` | `Q-###` for any readiness/ownership blocker. |

## Rules

- **Proposal ≠ commitment.** No backlog status changes here.
- **Qualified refs mandatory.**
- **Capacity is a ceiling.** No over-commit.
- **Readiness gate enforced.** Unsizable/low-confidence items are excluded, not squeezed in.

## Example

Eligible: `employee-portal:BKL-001` (M, high), `helpdesk:BKL-001` (M, high), `employee-portal:BKL-003` (S, medium, depends on `employee-portal:BKL-002` — not in scope → excluded). Budget ~17 ideal-days. Proposed: the two M items (~10 days). Goal: *"Ship SSO + ticket-import across the portal and helpdesk."* Status: **proposed** — awaiting human approval.
