---
doc_type: memory
memory_type: requirements
project: sample-employee-portal
last_reviewed: 2026-07-10
counter: 2
---

# Requirements — Acme Employee Portal

> ⚠️ Fictional sample. `REQ-001` was extracted by Meeting Intelligence, then **refined and promoted to `accepted`** by Requirements Management (Phase 2). `REQ-002` is a **draft** proposed by Backlog Ingestion (P3 step 1b) for the previously un-traced FEAT-002 (Payslip Viewer) — still `proposed`.

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

### REQ-002 — Payslip Viewer (current and historical payslips)

---
id: REQ-002
title: Payslip Viewer (current and historical payslips)
statement: The employee portal shall let employees view their current and historical payslips and export a payslip as PDF, covering FEAT-002.
type: functional
status: proposed
priority: medium
phase: 1
feature: [FEAT-002]
source: [SRC-BKL-2026-07-10]
owners: [ACTOR-002]
acceptance:
  - Employees can view current and historical payslips.
  - Employees can export a payslip as PDF.
  - An empty state is shown when no payslip exists.
assumptions: [ASM-001]
rationale: Draft proposed during Backlog Ingestion of the Payslip roadmap raw backlog (SRC-BKL-2026-07-10) — FEAT-002 previously had no requirement. Not yet accepted.
tags: [payslip, viewer, export]
created: 2026-07-10
updated: 2026-07-10
supersedes: []
superseded_by: []
relates_to: [FEAT-002, BKL-003, BKL-004]
---

Draft proposed by Backlog Ingestion (Step 1b) from `SRC-BKL-2026-07-10`, because FEAT-002 (Payslip Viewer) had no requirement. Still `proposed` — not backlog-eligible (as accepted) until signed off.

## Superseded / Rejected
*(none yet)*

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Created REQ-001 (counter=1). | Extraction from SRC-MTG-2026-06-15. |
| 2026-06-16 | agent | Refined REQ-001 → `accepted` (statement, acceptance, rationale, assumption ASM-001). | Requirements Management — Refinement. |
| 2026-07-10 | agent | Created REQ-002 (counter=2). | Backlog Ingestion (SRC-BKL-2026-07-10) — draft REQ for un-traced FEAT-002. |
