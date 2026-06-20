---
doc_type: knowledge
knowledge_type: scope
project: sample-employee-portal
last_reviewed: 2026-06-15
---

# Scope — Acme Employee Portal

> ⚠️ Fictional sample.

## Phases

### Phase 1 — MVP (target 2026-08-01)
- **In scope:**
  - MOD-002 Identity (SSO via Okta) — live by July.
  - MOD-001 Employee Portal Core:
    - FEAT-001 SSO Login
    - FEAT-002 Payslip Viewer
    - FEAT-003 Leave Request Submission (submit-only, no approvals)
- **Out of scope:**
  - Manager approval workflows (BR-002).
  - Native mobile applications.
  - Contractor access entitlement (unresolved — Q-002).

## Global Out-of-Scope
- Native mobile apps — web-first strategy for now.
- Third-party/vendor self-service — internal employees only (contractors pending Q-002).

## Scope Decisions
| Date | Decision | Impact | Source |
|------|----------|--------|--------|
| 2026-06-15 | DEC-001 — Adopt Okta for SSO | Sets Identity approach; enables July pilot. | SRC-MTG-2026-06-15 |

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Defined Phase 1 scope. | Onboarding (SRC-MTG-2026-06-15). |
