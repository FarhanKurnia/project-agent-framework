---
doc_type: knowledge
knowledge_type: features
project: sample-employee-portal
last_reviewed: 2026-07-10
---

# Features — Acme Employee Portal

> ⚠️ Fictional sample. Phase-1 feature set.

## FEAT-001 — Single Sign-On (SSO) Login
- **Module:** MOD-002 (Identity)
- **Serves:** ACTOR-001 (employees)
- **Description:** Employees authenticate to the portal via corporate SSO backed by Okta — no separate portal password.
- **Key requirements:** REQ-001
- **Status:** accepted

## FEAT-002 — Payslip Viewer
- **Module:** MOD-001 (Employee Portal Core)
- **Serves:** ACTOR-001
- **Description:** Employees view current and historical payslips.
- **Key requirements:** REQ-002 (proposed)
- **Status:** proposed

## FEAT-003 — Leave Request Submission
- **Module:** MOD-001 (Employee Portal Core)
- **Serves:** ACTOR-001
- **Description:** Employees submit leave requests (no manager approval in phase 1).
- **Key requirements:** *(to be extracted)*
- **Status:** proposed

## Feature → Module matrix
| Feature | Module | Primary actor | Status |
|---------|--------|---------------|--------|
| FEAT-001 | MOD-002 | ACTOR-001 | accepted |
| FEAT-002 | MOD-001 | ACTOR-001 | proposed |
| FEAT-003 | MOD-001 | ACTOR-001 | proposed |

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Added FEAT-001/002/003. | Onboarding (SRC-MTG-2026-06-15). |
| 2026-07-10 | agent | FEAT-002 key requirement = REQ-002 (proposed). | Backlog Ingestion (SRC-BKL-2026-07-10) — draft REQ linked. |
