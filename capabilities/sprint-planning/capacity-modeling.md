# Step 1 — Capacity Modeling

> Part of [Sprint Planning](README.md). Run first, at sprint start.

## Purpose

Compute the team's **capacity budget** for the sprint window — accounting for people, time, holidays, and absences — so the proposal (step 2) commits a realistic amount of work.

## Inputs

- `knowledge/actors.md` — team members who can take work (persons + teams).
- **Sprint window** — start and end dates (from the user or a cadence).
- **Holidays / absences** — public holidays, PTO, other commitments (from the user or a team calendar).
- Prior `outputs/sprints/*` — historical **velocity** (points completed per sprint), if any.

## Procedure

1. **Enumerate contributors** — the persons (and their availability %) who will work this sprint, from `knowledge/actors.md`. Note roles only where they constrain assignment (e.g., only one backend engineer).
2. **Compute available time** — for each contributor: working days in the window − holidays − absences × availability %. Sum to a team total.
3. **Apply a focus factor** — subtract a realistic margin for meetings, support, and overhead (commonly ~20–30%); state the factor used.
4. **Convert to a budget**:
   - If **velocity** exists (from prior sprints), express the budget in **points**.
   - If not, express in **ideal person-days/hours** and flag it as an estimate.
5. **Record assumptions** as `ASM-###` (e.g., "no one is on PTO in week 2") so capacity can be re-checked.
6. **Write** the capacity budget into the sprint artifact (step 2 creates the file; or note it for the proposal).

## Outputs

| Artifact | Notes |
|----------|-------|
| Capacity budget | Recorded in the sprint artifact's *Capacity* section (contributors, window, deductions, focus factor, total budget in points or days). |
| `memory/assumptions.md` | `ASM-###` for each capacity assumption. |

## Rules

- **Honest capacity.** Do not inflate. Holidays/absences/focus factor are subtracted, not ignored.
- **Velocity is historical, not aspirational.** Use the average of recent sprints; if volatile, use the lower bound and flag it.
- **No velocity → estimate + flag.** First sprints have no history; state the budget as an estimate and revisit after the sprint.
- **Assumptions explicit.** Capacity rests on assumptions (availability, no interruptions); record them as `ASM-###`.

## Example

Window 2026-07-06 → 2026-07-19 (10 working days). Team: Ben (ACTOR-002, 100%), Dana (ACTOR-003, 50%). One public holiday (2026-07-17). Focus factor 25%. Prior velocity: ~6 points/sprint.

- Ben: 10 − 1 = 9 days. Dana: (10 − 1) × 50% = 4.5 days. Raw total = 13.5 days.
- After 25% focus: ~10 ideal days.
- Budget: **6 points** (anchored to velocity), ~10 ideal days available.
- Assumption `ASM-002`: "No unplanned PTO during the window."
