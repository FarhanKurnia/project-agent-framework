---
doc_type: knowledge
knowledge_type: business-rules
project: sample-employee-portal
last_reviewed: 2026-06-15
---

# Business Rules — Acme Employee Portal

> ⚠️ Fictional sample.

## BR-001 — Corporate SSO standard
- **Category:** policy
- **Statement:** All internal Acme applications must authenticate via corporate SSO; standalone application passwords are not permitted.
- **Rationale:** Security standardization; established by IT. Underpins DEC-001.
- **Applies to:** FEAT-001, MOD-002
- **Source:** SRC-MTG-2026-06-15
- **Exceptions:** none

## BR-002 — Phase-1 has no manager approvals
- **Category:** constraint
- **Statement:** Manager approval workflows are excluded from Phase 1 scope; the portal supports submit-only flows until a later phase.
- **Rationale:** Stated scope decision in kickoff.
- **Applies to:** FEAT-003
- **Source:** SRC-MTG-2026-06-15
- **Exceptions:** none

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Added BR-001/002. | Onboarding (SRC-MTG-2026-06-15). |
