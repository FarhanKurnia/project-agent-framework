# Step 3 — Load Reconciliation

> Part of [Profile Management](README.md). Keeps `current_load` trustworthy for Portfolio Sprint Planning.

## Purpose
Recompute each `PERSON-###`'s `current_load` from all in-flight portfolio sprints, so the per-person capacity ceiling and skill assignment use real committed load.

## Inputs
- `portfolio/profiles/team.md` (all `PERSON-###`).
- All `portfolio/sprints/sprint-PS-NN-*.md` at `status: committed` (not `closed`).

## Procedure
1. **Collect in-flight sprints** — every portfolio sprint with frontmatter `status: committed`.
2. **For each `PERSON-###`**, sum the effort of items assigned to them across those sprints:
   - Read each committed sprint's *Committed Scope*; for rows where `owner: <PERSON-###>`, add the item's `size` (convert t-shirt → points: S=2, M=3, L=5) or ideal-days.
3. **Compute `current_load`** as a % of the person's capacity: `current_load = min(100, round(100 * committed / capacity))`, where `capacity` is that person's budget share across the in-flight window(s) (availability % × net working days × (1 − focus)).
4. **Write** `current_load:` back to each PERSON in `team.md`; bump `updated` only if it changed; changelog row "Reconciled current_load."
5. **Report** per-person load; flag any PERSON > 100% (overcommitted → raise `Q-###`).

## Rules
- **Derived, not hand-set.** `current_load` is always recomputed here, never guessed.
- **Only in-flight sprints count** — closed sprints don't consume current capacity.
- **Overload is a signal** — a PERSON > 100% means the portfolio is overcommitted on them; raise `Q-###`.

## Example
PERSON-001 owns `helpdesk:BKL-001` (M=3) in PS-01 (committed). Capacity share ~6 points over the window. 1 sprint in flight, 3 points committed → `current_load ≈ 50%`. Write back; flag if > 100.
