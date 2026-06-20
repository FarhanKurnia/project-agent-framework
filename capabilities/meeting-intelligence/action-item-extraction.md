# Step 6 — Action Item Extraction

> Part of [Meeting Intelligence](README.md). Run after [Meeting Analysis](meeting-analysis.md), alongside the other extraction steps.

## Purpose

Convert action item candidates from the analysis into formal `ACT-###` items in `memory/action-items.md`, each with a **single accountable owner** and a **due date** where stated.

## Inputs

- The in-session analysis (action item candidates).
- `memory/action-items.md` (current items + `counter`).
- `knowledge/actors.md` (to resolve owners to `ACTOR-###`).

## Procedure

1. **Load** existing action items into a lookup (by owner + action description).
2. **For each action candidate**:
   1. **Resolve the owner** to an `ACTOR-###` (or note an unrecognized attendee for Knowledge update). If the owner is ambiguous, raise a `Q-###` ("Who owns <action>?") and leave `owner: <unresolved>`.
   2. **Search** for an existing item covering the same commitment by the same owner.
      - Match → **update** (refine description, due date, status), append source, bump `updated`. Note reconciliation.
      - No match → **create** a new `ACT-###` (increment `counter`) with `description`, `status: open`, `owner`, `due` (if stated), `priority`, `source: [<meeting_id>]`, `relates_to`, dates.
   3. If a **due date** is not stated, leave `due:` blank and consider raising a `Q-###` ("When is ACT-### due?") for high-priority items.
3. **Link** each action item to the decision/requirement it serves (`relates_to`).
4. **Record reconciliations** for the MOM.
5. **Write** the updated `memory/action-items.md`.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/action-items.md` | New/updated `ACT-###` items; counter updated. |
| Reconciliation notes | Fed into the MOM. |

## Rules

- **Single owner.** Each action item has exactly one accountable owner. "Finance team" is acceptable as a team actor (`ACTOR-T###`), but "Alice and Bob" should be split into two items.
- **Provenance required.** `source: [<meeting_id>]`.
- **Owner ambiguity → question.** Do not assign an owner you cannot identify; raise a `Q-###`.
- **Due dates are optional but tracked.** Missing due dates on high-priority items are flagged.
- **Never delete.** Mark `done`/`dropped` with a `resolution` note.
- **Reconcile-first.** The same recurring task across standups is one action item (updated), not many.

## Example

Candidate: *"Alice, can you confirm the IdP licenses by next Friday?"* (Alice = `ACTOR-001`, next Friday = 2026-06-27.)

No existing match → create `ACT-001`:

```markdown
### ACT-001 — Confirm Okta IdP licenses

---
id: ACT-001
title: Confirm Okta IdP licenses
description: Confirm the number and cost of Okta IdP licenses required for the employee portal.
status: open
owner: ACTOR-001
supporters: []
due: 2026-06-27
priority: high
source: [SRC-MTG-2026-06-15]
relates_to: [DEC-001, REQ-001]
resolution:
created: 2026-06-15
updated: 2026-06-15
---
```
