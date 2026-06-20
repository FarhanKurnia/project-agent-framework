---
doc_type: memory
memory_type: decisions
project: sample-employee-portal
last_reviewed: 2026-06-15
counter: 1
---

# Decisions — Acme Employee Portal

> ⚠️ Fictional sample. Extracted from SRC-MTG-2026-06-15.

## Active Decisions

### DEC-001 — Adopt Okta as SSO/IdP

---
id: DEC-001
title: Adopt Okta as SSO/IdP
status: accepted
context: The employee portal needs an authentication mechanism; Acme must choose an identity approach consistent with corporate standards.
decision: Use Okta as the identity provider for portal SSO.
rationale: Okta is already the corporate standard (BR-001); avoids onboarding a new vendor and reuses existing IT investment.
consequences: Okta licenses required (count TBD — ACT-001); Identity module (MOD-002) integration effort.
scope: project-wide
source: [SRC-MTG-2026-06-15]
deciders: [ACTOR-001, ACTOR-002]
affects: [REQ-001, FEAT-001, MOD-002]
tags: [auth, sso]
created: 2026-06-15
updated: 2026-06-15
supersedes: []
superseded_by: []
---

Agreed by Alice (ACTOR-001) and Ben (ACTOR-002) in the kickoff. Enables the July SSO target.

## Superseded / Rejected
*(none yet)*

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Created DEC-001 (counter=1). | Extraction from SRC-MTG-2026-06-15. |
