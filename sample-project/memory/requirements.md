---
doc_type: memory
memory_type: requirements
project: sample-employee-portal
last_reviewed: 2026-06-15
counter: 1
---

# Requirements — Acme Employee Portal

> ⚠️ Fictional sample. Items below were extracted from SRC-MTG-2026-06-15.

## Open / Accepted Requirements

### REQ-001 — Employee portal SSO via Okta

---
id: REQ-001
title: Employee portal SSO via Okta
statement: The employee portal shall authenticate users via corporate SSO backed by Okta, with SSO live by July 2026 to enable pilot onboarding.
type: functional
status: proposed
priority: high
feature: [FEAT-001]
source: [SRC-MTG-2026-06-15]
owners: [ACTOR-002]
acceptance: [Employees log in with corporate SSO credentials, No separate portal password exists, SSO operational by July 2026]
tags: [auth, sso]
created: 2026-06-15
updated: 2026-06-15
supersedes: []
superseded_by: []
relates_to: [DEC-001, ACT-001, ACT-002]
---

Driven by business rule BR-001 (corporate SSO standard) and decision DEC-001 (adopt Okta). Pilot onboarding depends on this being live by July.

## Superseded / Rejected
*(none yet)*

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Created REQ-001 (counter=1). | Extraction from SRC-MTG-2026-06-15. |
