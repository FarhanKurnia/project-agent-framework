# Knowledge — Modules (Template)

> Copy into `projects/<project>/knowledge/modules.md`.
> **Modules** are the functional building blocks of the solution. Stable and high-level.

---
doc_type: knowledge
knowledge_type: modules
project: <project-slug>
last_reviewed: <YYYY-MM-DD>
---

# Modules — <Project Name>

> Each module has a `MOD-###` ID. Features (`FEAT-###` in `features.md`) group under modules.

## MOD-001 — <Module Name>
- **Purpose:** <one line — what this module is responsible for>
- **Key actors:** <ACTOR-###>
- **Owning team:** <ACTOR-T###>
- **Status:** <planned / in-design / in-build / live>
- **Features:** <FEAT-###, FEAT-###>
- **Notes:** <integration points, dependencies>

## MOD-002 — <Module Name>
- … *(copy block per module)*

## Module Map
<Optional: a simple text diagram of how modules relate.>

```
<MOD-001> ──▶ <MOD-002> ──▶ <MOD-003>
```

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | <name> | Added MOD-001/002. | Onboarding (<SRC-…>). |
