# Step 4 — Open Questions Report

> Part of [Reporting](README.md). Run on demand or each period.

## Purpose

Show every **unresolved question**, how long it has been open, who must answer it, and which ones are **blocking** work — so stale and blocking questions get resolved instead of forgotten.

## Inputs

- `memory/open-questions.md` — `Q-###` with `created`, `priority`, `needs_answer_from`, `blocks`.

## Procedure

1. **Compute age** for each open `Q-###`: `today − created` (use the known current date).
2. **Sort** by `priority` (blocking → high → medium → low), then by age (oldest first).
3. **Render the list** — per `Q-###`: question, age (days), priority, `needs_answer_from`, `blocks:`.
4. **Flag stale** — questions open longer than the project's threshold (default **14 days**) are marked ⏳ stale and need escalation.
5. **Highlight blockers** — any `Q-###` with non-empty `blocks:` is a blocker; surface at top.
6. **Recently closed** — questions answered this period, with the answer summary.
7. **Gap check** — an area with many blocking questions may indicate a missing decision → raise `Q-###` or flag for a `DEC`.

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/reports/open-questions-<YYYY-MM-DD>.md` | Regenerable. |
| `memory/open-questions.md` | Optional: no status changes from reporting (closing happens where the answer lands). |

## Rules

- **Age is computed from `created`.** Use the current date; do not guess.
- **Blocking questions lead.** They gate requirements/decisions and must be visible.
- **Cite IDs.** Each row links to its `Q-###` and what it `blocks:`.
- **Read-only upstream.**

## Example

| Q | Question | Age | Priority | Needs answer | Blocks |
|---|----------|-----|----------|--------------|--------|
| Q-002 | Do contractors get portal access? | 21d ⏳ | high/blocking | ACTOR-001 | REQ-001, DEC-001 |
| Q-001 | When is the Identity design due? | 21d | high | ACTOR-002 | ACT-002 |
