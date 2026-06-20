# Step 2 — Sprint Proposal

> Part of [Sprint Planning](README.md). Run after [Capacity Modeling](capacity-modeling.md). Produces a **recommendation** — not a commitment.

## Purpose

Recommend a sprint set from the ready backlog that respects **priority, dependencies, and capacity**, with a clear sprint goal and an explicit list of what did not fit.

## Inputs

- `memory/backlog.md` — items at `status: ready` (sized, `confidence ≥ medium`, dependency-linked).
- Capacity budget from step 1.
- `memory/decisions.md` — priorities/method (e.g., MoSCoW) and any sequencing decisions.
- `memory/assumptions.md` — capacity assumptions.

## Procedure

1. **Filter to eligible items**: `status: ready`, `size` set, `confidence ≥ medium`. Exclude `new`/unsizable/low-confidence items (they are carry-forward candidates or `Q-###`).
2. **Order** eligible items: by `priority` (critical → low), then by **dependency** (a blocker before its blocked items), then by `size` (to pack the budget).
3. **Select greedily within capacity**: pull items in order until the cumulative `size` reaches the budget. Stop when the next item would exceed it.
4. **Respect dependencies absolutely**: never include a blocked item whose blocker is **not** also in this sprint (or already delivered). Such items are deferred with the reason "blocked by BKL-###".
5. **Draft a sprint goal** — one sentence capturing the outcome this sprint delivers (tie it to a phase goal in `knowledge/scope.md`).
6. **List carry-forward candidates** — high-priority items that did not fit, flagged for the next sprint.
7. **List exclusions with reasons** — items deliberately left out (blocked, not ready, low priority).
8. **Write** `outputs/sprints/sprint-<n>-<date>.md` from the template (status: **proposed**), with capacity, proposed scope, goal, carry-forwards, exclusions.
9. **Stop for human approval** before step 3 (commitment).

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/sprints/sprint-<n>-<date>.md` | Proposed sprint (status: proposed). |
| `memory/open-questions.md` | `Q-###` for any item whose readiness/ownership blocks inclusion. |

## Rules

- **Proposal ≠ commitment.** No backlog status changes here; that happens at commitment (step 3).
- **Capacity is a ceiling.** The proposed set must fit the budget; never over-commit.
- **Dependencies govern order.** The critical path is honored; blocked items wait.
- **Readiness gate enforced.** Unsizable/low-confidence items are excluded, not squeezed in.
- **Goal ties to scope.** The sprint goal must be supportable by the proposed set; if not, reshape the set or the goal.

## Example

Eligible & ordered: BKL-001 (Okta SSO integration, M, critical, no deps) → BKL-002 (portal login UI, S, high, depends on BKL-001). Budget 6 points (~M+S fit).

Proposed: **BKL-001** (M, ~3pt) + **BKL-002** (S, ~2pt). Goal: *"Employees can sign in to the portal via Okta SSO."*
Carry-forward: *(none this sprint)*.
Excluded: BKL-003 (contractor access) — depends on unresolved `Q-002`.

Status: **proposed** — awaiting human approval to commit.
