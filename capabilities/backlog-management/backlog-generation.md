# Step 1 — Backlog Generation

> Part of [Backlog Management](README.md). Run first to stand up the backlog.

## Purpose

Derive formal `BKL-###` items from **accepted requirements** and **recurring action items**, so the project has an explicit, traceable list of work to deliver.

## Inputs

- `memory/requirements.md` — only items at `status: accepted` (proposed requirements are **not** backlog-eligible yet).
- `memory/action-items.md` — recurring or deliverable action items (e.g., "draft design", "build integration") that represent units of work.
- `knowledge/features.md` and `knowledge/modules.md` — to set `delivers: [FEAT-###]`.
- `memory/backlog.md` — current backlog + `counter`.

## Procedure

1. **Collect origins**: enumerate every accepted `REQ-###` and every recurring/deliverable `ACT-###`.
2. **Load** existing backlog items into a lookup (by `derived_from` and title).
3. **For each origin**:
   1. **Search** for an existing `BKL-###` already derived from this same origin.
      - Match → **update** (refine description, status) and bump `updated`. Note reconciliation.
      - No match → **create** a new `BKL-###` (increment `counter`):
        - `derived_from: [REQ-###]` (and/or `[ACT-###]`)
        - `delivers: [FEAT-###]` — the feature this work produces (from Knowledge)
        - `description` — the work as a deliverable, not a restatement of the requirement
        - `status: new`, `priority:` *(set in step 2)*, `size:` *(step 3)*, `confidence:` *(step 3)*
        - `source: [<origin's source>]` (carry provenance forward)
        - dates
   2. **Decompose when needed.** A large requirement may need **multiple** `BKL-###` items (e.g., one per module). If so, create one item per meaningful chunk and link all back to the same `derived_from`.
   3. **One-to-one default, one-to-many when justified.** Prefer one backlog item per requirement; split only when the requirement clearly spans independent deliverables.
4. **Flag orphans**: a backlog item with no `delivers:` feature means Knowledge is incomplete — raise a `Q-###` ("which feature does BKL-### deliver?") rather than leaving it unlinked.
5. **Write** the updated `memory/backlog.md`, placing items under "New / Ready".

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/backlog.md` | New/updated `BKL-###`; counter updated. |
| Orphan flags | `Q-###` for any item lacking a `delivers:` link. |

## Rules

- **Accepted only.** Never generate backlog from `proposed`/`superseded` requirements. If a requirement should be promoted, that is a separate decision (record a `DEC-###` and set `REQ-###.status: accepted` first).
- **Provenance carried forward.** `source:` on the backlog item = the origin's source.
- **Reconcile-first.** One origin → at most one set of backlog items; do not regenerate duplicates on re-runs.
- **Never delete.** Close delivered items in step 5.

## Example

Origin: `REQ-001` (accepted) — "Employee portal SSO via Okta, live by July." It delivers `FEAT-001` (SSO Login) in `MOD-002` (Identity).

No existing backlog item → create `BKL-001`:

```markdown
### BKL-001 — Implement Okta SSO integration (Identity module)

---
id: BKL-001
title: Implement Okta SSO integration (Identity module)
description: Build the Identity module (MOD-002) integration with Okta so employees authenticate via corporate SSO; deliver FEAT-001.
status: new
priority: high
size: M
confidence: medium
derived_from: [REQ-001, ACT-002]
delivers: [FEAT-001]
owner:
sprint: none
dependencies: []
source: [SRC-MTG-2026-06-15]
created: 2026-06-15
updated: 2026-06-15
---
```

If `REQ-001` later also implied a separate "contractor access" deliverable, that would be a **second** item `BKL-002`, both `derived_from: [REQ-001]`, but delivering different features.
