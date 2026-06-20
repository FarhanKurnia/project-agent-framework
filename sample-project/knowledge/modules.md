---
doc_type: knowledge
knowledge_type: modules
project: sample-employee-portal
last_reviewed: 2026-06-15
---

# Modules — Acme Employee Portal

> ⚠️ Fictional sample.

## MOD-001 — Employee Portal (Core)
- **Purpose:** The web front-end employees use to self-service HR tasks.
- **Key actors:** ACTOR-001 (employees), ACTOR-S01 (Okta)
- **Owning team:** ACTOR-T01 (HR) for product; ACTOR-002 for build
- **Status:** planned
- **Features:** FEAT-001, FEAT-002, FEAT-003
- **Notes:** Depends on MOD-002 for authentication.

## MOD-002 — Identity
- **Purpose:** Authentication and authorization via corporate SSO (Okta).
- **Key actors:** ACTOR-S01 (Okta)
- **Owning team:** ACTOR-002 (Tech Lead)
- **Status:** planned
- **Features:** FEAT-001
- **Notes:** Must be live by July 2026 to enable pilot. Design draft owed by Ben (ACT-002).

## Module Map
```
[Employee: ACTOR-001] ──▶ MOD-001 Employee Portal ──▶ MOD-002 Identity ──▶ ACTOR-S01 Okta
```

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Added MOD-001/002. | Onboarding (SRC-MTG-2026-06-15). |
