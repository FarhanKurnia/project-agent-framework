# Knowledge — Scope (Template)

> Copy into `projects/<project>/knowledge/scope.md`.
> **Scope** records what is in and out of the delivery, by phase. The primary defense against scope creep.

---
doc_type: knowledge
knowledge_type: scope
project: <project-slug>
last_reviewed: <YYYY-MM-DD>
---

# Scope — <Project Name>

## Phases
> Organize delivery into phases. Each phase lists the modules/features delivered and explicitly excluded.

### Phase 1 — <Name> (e.g. MVP)
- **In scope:** <MOD-### / FEAT-### / capability>
- **Out of scope:** <explicitly named exclusions>
- **Target:** <YYYY-MM-DD>

### Phase 2 — <Name>
- **In scope:** …
- **Out of scope:** …

## Global Out-of-Scope
<Items excluded for the entire project, with a one-line reason.>

- <Item> — <reason>

## Scope Decisions
<Decisions that changed scope. Link DEC-### and the source that triggered it.>

| Date | Decision | Impact | Source |
|------|----------|--------|--------|
| <YYYY-MM-DD> | <DEC-### summary> | <added/removed X> | <SRC-…> |

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | <name> | Defined Phase 1 scope. | Onboarding (<SRC-…>). |
