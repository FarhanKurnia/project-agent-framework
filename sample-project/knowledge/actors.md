---
doc_type: knowledge
knowledge_type: actors
project: sample-employee-portal
last_reviewed: 2026-06-15
---

# Actors — Acme Employee Portal

> ⚠️ Fictional sample. IDs are scoped to this project.

## Persons
### ACTOR-001 — Alice Chen
- **Role:** Product Owner
- **Kind:** person
- **Contact:** alice@acme.example
- **Responsibility:** Owns product scope and HR policy decisions.
- **Mentioned in:** SRC-MTG-2026-06-15

### ACTOR-002 — Ben Park
- **Role:** Tech Lead
- **Kind:** person
- **Contact:** ben@acme.example
- **Responsibility:** Owns technical architecture and the Identity module.
- **Mentioned in:** SRC-MTG-2026-06-15

### ACTOR-003 — Dana Lee
- **Role:** HR Analyst
- **Kind:** person
- **Contact:** dana@acme.example
- **Responsibility:** HR operations liaison; raised contractor-access question.
- **Mentioned in:** SRC-MTG-2026-06-15

## Teams
### ACTOR-T01 — HR Team
- **Kind:** team
- **Lead:** ACTOR-003 (Dana Lee)
- **Responsibility:** Owns HR processes the portal supports.

## Systems
### ACTOR-S01 — Okta (Identity Provider)
- **Kind:** system
- **Owner:** Acme IT
- **Purpose:** Corporate identity provider; backs SSO for the portal.
- **Integrates with:** Employee Portal (MOD-001)

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Added ACTOR-001/002/003, T01, S01. | Onboarding (SRC-MTG-2026-06-15). |
