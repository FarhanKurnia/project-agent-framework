---
doc_type: memory
memory_type: assumptions
project: sample-employee-portal
last_reviewed: 2026-07-06
counter: 2
---

# Assumptions — Acme Employee Portal

> ⚠️ Fictional sample. Populated by Requirements Management (ASM-001) and Sprint Planning (ASM-002).

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

### ASM-002 — No unplanned PTO during Sprint S-01

---
id: ASM-002
title: No unplanned PTO during Sprint S-01
statement: No contributor takes unplanned leave during the S-01 window (2026-07-06 → 2026-07-17) beyond the known public holiday.
status: open
impacts: [BKL-001, BKL-002]
source: [SRC-MTG-2026-06-15]
rationale: The S-01 capacity budget (Sprint Planning) assumes full availability minus the known holiday.
validated_by:
invalidated_by:
created: 2026-07-06
updated: 2026-07-06
---

If violated, S-01 capacity is reduced and BKL-002 may slip to the next sprint.

## Validated
*(none yet)*

## Invalidated
*(none yet)*

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-16 | agent | Created ASM-001 (counter=1). | Requirements Management — Refinement of REQ-001. |
| 2026-07-06 | agent | Created ASM-002 (counter=2). | Sprint Planning — Capacity Modeling for S-01. |
