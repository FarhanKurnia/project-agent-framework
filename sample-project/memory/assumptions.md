---
doc_type: memory
memory_type: assumptions
project: sample-employee-portal
last_reviewed: 2026-06-16
counter: 1
---

# Assumptions — Acme Employee Portal

> ⚠️ Fictional sample. Populated by Requirements Management (Refinement). Each assumption is a `ASM-###`.

## Open Assumptions

### ASM-001 — Okta licensing covers all portal users

---
id: ASM-001
title: Okta licensing covers all portal users
statement: The Okta license count (once confirmed via ACT-001) will be sufficient for all employee-portal users, including the pilot cohort.
status: open
impacts: [REQ-001]
source: [SRC-MTG-2026-06-15]
rationale: REQ-001's July pilot target assumes no licensing shortfall; license count is still pending (ACT-001, due 2026-06-27).
validated_by:
invalidated_by:
created: 2026-06-16
updated: 2026-06-16
---

If ACT-001 reveals a shortfall, this assumption moves to `invalidated` and Drift Detection re-examines REQ-001.

## Validated
*(none yet)*

## Invalidated
*(none yet)*

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-16 | agent | Created ASM-001 (counter=1). | Requirements Management — Refinement of REQ-001. |
