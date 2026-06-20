# Memory — Assumptions (Template)

> Copy into `projects/<project>/memory/assumptions.md`.
> **Assumptions** are things a requirement treats as true without proof. If invalidated, the requirements that rest on them are at risk — so assumptions are first-class, citable, and explicitly validated.

---
doc_type: memory
memory_type: assumptions
project: <project-slug>
last_reviewed: <YYYY-MM-DD>
counter: 0
---

# Assumptions — <Project Name>

> Each assumption is an `ASM-###`. Lifecycle: `open → validated | invalidated`.
> Populated mainly by Requirements Management (Refinement). Linked from requirements via `assumptions: [ASM-###]`.

<!-- TEMPLATE FOR A NEW ITEM:
### ASM-001 — <short title>

---
id: ASM-001
title: <short title>
statement: <what is assumed to be true, stated precisely>
status: open                             # open | validated | invalidated
impacts: [REQ-###]                       # requirements that rest on this
source: [<SRC-…>]                        # REQUIRED provenance (where the assumption was made)
rationale: <why we assume this>          # optional
validated_by: <how/when/who confirmed>   # filled when status -> validated
invalidated_by: [<evidence>]             # filled when status -> invalidated (then re-run Drift Detection)
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---

<Optional detail.>
-->

## Open Assumptions

<!-- not yet validated -->

## Validated

<!-- confirmed true -->

## Invalidated

<!-- confirmed false -> triggers Drift Detection on every REQ in `impacts:` -->

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | <name> | Created file (counter=0). | Refinement (<SRC-…>). |
