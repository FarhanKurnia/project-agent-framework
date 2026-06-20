# Step 2 — Profile Maintenance

> Part of [Profile Management](README.md).

## Purpose
Update an existing `PERSON-###` (skills, level, availability, status) or supersede one (departure → `alumni`).

## Inputs
- `portfolio/profiles/team.md`.
- A change source (role change, PTO, departure).

## Procedure
1. **Locate** the `PERSON-###` by id/name.
2. **Edit fields** (skills, level, availability, contact); bump `updated`; add a changelog row.
3. **Status transitions:**
   - Part-time / on leave → `status: part-time` or `unavailable` (reduce availability).
   - Departure → `status: alumni` (keep the item + history; **do not delete**).
   - Return → `status: active`.
4. **Report** the change.

## Rules
- **Never delete — supersede.** A leaver becomes `alumni`; their `PERSON-###` is never reused.
- **`current_load` is not hand-edited here** — use [load-reconciliation](load-reconciliation.md).
- **Provenance** for material changes (e.g. a role change) cites the source.

## Example
PERSON-002 goes part-time (50%): set `availability: 50`, `status: part-time`, bump `updated`, changelog "Reduced to 50% per `<source>`."
