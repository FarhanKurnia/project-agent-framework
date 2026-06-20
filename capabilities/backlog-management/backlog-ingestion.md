# Step 1b — Backlog Ingestion (from a raw backlog source)

> Part of [Backlog Management](README.md). An **alternate entry point** to [Step 1 Generation](backlog-generation.md): instead of deriving `BKL-###` from accepted requirements, ingest a **raw backlog** a stakeholder already wrote (planning dump, spreadsheet, roadmap draft).

## Purpose

Turn an informal, externally-authored backlog (`source/backlog/*.md`) into formal, traceable `BKL-###` items — while preserving provenance and restoring the framework's traceability (every item traces to a feature, and to a requirement where one exists).

This is the **bottom-up** path; Generation is the **top-down** path. Use whichever matches where the work actually starts. Both feed the same downstream steps (Prioritization → Estimation → Dependency Mapping → Grooming).

## Inputs

- `source/backlog/<file>.md` — the raw backlog (immutable source). Its `backlog_id` (e.g. `SRC-BKL-2026-06-20`) is the provenance for everything extracted.
- `knowledge/features.md`, `knowledge/modules.md` — to set `delivers: [FEAT-###]` / map to `MOD-###`.
- `memory/requirements.md` — to link items to existing `REQ-###`.
- `memory/backlog.md` — current backlog + `counter` (reconcile against it).
- `memory/decisions.md`, `memory/open-questions.md`, `memory/assumptions.md` — raw backlogs often embed decisions, questions, and assumptions.

## Procedure

1. **Parse** the raw backlog into discrete work items (one logical deliverable each).
2. **Load** existing `BKL-###` into a lookup (by title + source) to avoid duplicates.
3. **For each parsed item**:
   1. **Reconcile** — if a `BKL-###` already exists for this item (same source/title), **update** it and note reconciliation. Otherwise create a new `BKL-###` (increment `counter`).
   2. **Trace to a feature** — set `delivers: [FEAT-###]` from Knowledge where the item clearly maps; note the `MOD-###`.
   3. **Trace to a requirement** — if an existing `REQ-###` covers it, set `derived_from: [REQ-###]`.
   4. **Un-traced handling (the key rule)** — if the item maps to **no** FEAT and **no** existing REQ, do **not** leave it dangling. Either:
      - **propose a draft `REQ-###`** (`status: proposed`, `source: [SRC-BKL-…]`) capturing the need it implies, and set `derived_from: [REQ-###]`; **or**
      - **raise a `Q-###`** ("which feature/requirement does this backlog item belong to?").
   5. **Carry fields already present** in the raw item — `priority`, `size`/estimate, `dependencies` (normalize into `dependencies`/`blockedBy`). Preserve as-is; Steps 2–4 refine them. If the raw item carries a tracker task id, set `external_ref`; its subtasks → the BKL `Subtasks:` checklist (manual two-way sync).
   6. **Provenance** — set `source: [SRC-BKL-…]`.
4. **Surface secondary extractions** — a raw backlog often encodes more than work items: a stated choice → `DEC-###`; an unknown/risk → `Q-###`; an unstated premise → `ASM-###`. All cite the `backlog_id`.
5. **Write** new/updated items to `memory/backlog.md` ("New / Ready"); write any new `REQ-###`/`DEC-###`/`Q-###`/`ASM-###` to their files; update counters.
6. **Continue the pipeline** — run Prioritization → Estimation → Dependency Mapping (Steps 2–4) to groom the ingested items.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/backlog.md` | New/updated `BKL-###`; counter updated. |
| `memory/requirements.md` | Draft `REQ-###` (proposed) for un-traced items that imply new scope. |
| `memory/decisions.md`, `memory/open-questions.md`, `memory/assumptions.md` | Secondary extractions, if any. |
| Traceability report | Per item: its FEAT/REQ link, or the `Q-###`/draft-`REQ-###` created to restore traceability. |

## Rules

- **Provenance mandatory.** Every extracted item cites `source: [SRC-BKL-…]`.
- **No dangling items.** Every ingested `BKL-###` must trace to a FEAT, and to a REQ (existing or a draft you propose) — or have an open `Q-###` asking where it belongs. This is the ingestion-specific form of "never invent work": the raw backlog is a cited origin, and traceability is **restored**, not skipped.
- **Reconcile-first.** Don't re-create items already in the backlog from the same source.
- **Draft REQs are proposals.** REQs synthesized during ingestion are `status: proposed` — they are NOT backlog-eligible until accepted (record a `DEC-###` and set `REQ-###.status: accepted` first). A `BKL-###` may still be created, but flag `source-status: proposed` when its REQ is still proposed.
- **Never delete — close.**
- **Execution tracker sync (manual, two-way).** If the raw backlog carries tracker task ids (e.g. `clickup:8612394`), set `external_ref` on the `BKL-###`; subtasks map to the BKL's `Subtasks:` checklist. PAF is the traceability layer, the tracker is execution — sync by `external_ref` as the join key.
- **One project only.** See `AGENTS.md` §7.

## Example

Raw item (from `source/backlog/2026-06-20-roadmap.md`, `backlog_id: SRC-BKL-2026-06-20`): *"Add a CSV export to the Ticket list — should be quick, needed before next month's demo."* — tagged `clickup:8612394`, with subtasks (filter query, column styling, unit test).

Knowledge map: Ticket list = `FEAT-005` (REQ-005 exists, `status: proposed`). No existing BKL for this.

→ Create `BKL-010`:

```markdown
### BKL-010 — CSV export for Ticket list (FEAT-005)

---
id: BKL-010
title: CSV export for Ticket list (FEAT-005)
description: Add CSV export to the Ticket list (FEAT-005); needed before next month's demo.
status: new
priority: high
size: S
confidence: medium
derived_from: [REQ-005]
delivers: [FEAT-005]
owner:
sprint: none
dependencies: []
external_ref: clickup:8612394     # ClickUp task id (manual two-way sync)
source: [SRC-BKL-2026-06-20]
source-status: proposed          # REQ-005 is still proposed
created: 2026-06-20
updated: 2026-06-20
---

Subtasks:
- [ ] active-filter query builder
- [ ] column header & footer styling
- [ ] export unit test
```

If instead the item implied scope with **no** matching FEAT/REQ (e.g. *"add WhatsApp notifications"*) → propose a draft `REQ-###` (proposed) and link it, or raise `Q-###`.
