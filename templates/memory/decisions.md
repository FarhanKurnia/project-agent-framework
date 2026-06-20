# Memory — Decisions (Template)

> Copy into `projects/<project>/memory/decisions.md`.
> **Decisions are living and cited.** Record the choice AND the rationale. Supersede, never delete.

---
doc_type: memory
memory_type: decisions
project: <project-slug>
last_reviewed: <YYYY-MM-DD>
counter: 0
---

# Decisions — <Project Name>

> Each decision is a `DEC-###`. Lightweight ADR-style: context, decision, rationale, consequences.
> Lifecycle: `proposed → accepted → superseded | rejected`. Use `supersedes` / `superseded_by` to keep history.

<!-- TEMPLATE FOR A NEW ITEM:
### DEC-001 — <short title>

---
id: DEC-001
title: <short title>
status: proposed                         # proposed | accepted | superseded | rejected
context: <why we needed to decide>       # the situation / forces
decision: <what we decided>              # the choice, stated plainly
rationale: <why this option>             # alternatives considered & why rejected
consequences: <impact, trade-offs>       # positive + negative
scope: <project-wide | module: MOD-###>
source: [<SRC-…>]                        # REQUIRED provenance (meeting/doc where decided)
deciders: [<name>]
affects: [REQ-###, FEAT-###]             # items this reshapes
tags: [<tag>]
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
supersedes: []
superseded_by: []
---

<Optional detail.>
-->

## Active Decisions

<!-- accepted / proposed items -->

## Superseded / Rejected

<!-- historical items, retained -->

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | <name> | Created file (counter=0). | Onboarding (<SRC-…>). |
