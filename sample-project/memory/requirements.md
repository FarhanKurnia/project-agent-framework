---
doc_type: memory
memory_type: requirements
project: sample-employee-portal
last_reviewed: 2026-06-16
counter: 1
---

# Requirements — Acme Employee Portal

> ⚠️ Fictional sample. `REQ-001` was extracted by Meeting Intelligence, then **refined and promoted to `accepted`** by Requirements Management (Phase 2).

## Open / Accepted Requirements

### REQ-001 — Employee portal SSO via Okta

---
id: REQ-001
title: Employee portal SSO via Okta
statement: The employee portal shall authenticate users via corporate SSO backed by Okta, with SSO operational by 2026-07-31 to enable pilot onboarding.
type: functional
status: accepted
priority: high
phase: 1
feature: [FEAT-001]
source: [SRC-MTG-2026-06-15]
owners: [ACTOR-002]
acceptance:
  - Employees sign in with corporate credentials; no separate portal password exists.
  - Okta issues the assertion consumed by the Identity module (MOD-002).
  - SSO is operational in a pilot environment by 2026-07-31.
assumptions: [ASM-001]
rationale: Gates the July pilot; corporate SSO standard (BR-001) + decision DEC-001 (adopt Okta).
tags: [auth, sso]
created: 2026-06-15
updated: 2026-06-16
supersedes: []
superseded_by: []
relates_to: [DEC-001, BR-001, ACT-001, ACT-002]
---

Refined by Requirements Management: statement made precise (deadline bound to 2026-07-31), acceptance criteria made testable, rationale and assumption recorded. Now eligible to feed Backlog Management.

## Superseded / Rejected
*(none yet)*

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Created REQ-001 (counter=1). | Extraction from SRC-MTG-2026-06-15. |
| 2026-06-16 | agent | Refined REQ-001 → `accepted` (statement, acceptance, rationale, assumption ASM-001). | Requirements Management — Refinement. |
