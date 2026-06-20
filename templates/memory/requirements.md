# Memory — Requirements (Template)

> Copy into `projects/<project>/memory/requirements.md`.
> **Memory is living and cited.** Every requirement MUST cite a source. Reconcile before adding; supersede, never delete.

---
doc_type: memory
memory_type: requirements
project: <project-slug>
last_reviewed: <YYYY-MM-DD>
counter: 0          # highest REQ number used; increment when adding
---

# Requirements — <Project Name>

> Each requirement is a `REQ-###` with its own frontmatter block below.
> Lifecycle: `proposed → accepted → superseded | rejected`. Trace to `FEAT-###` and cite `source:`.

<!-- TEMPLATE FOR A NEW ITEM — copy & fill:
### REQ-001 — <short title>

---
id: REQ-001
title: <short title>
statement: <the system shall…>          # one precise sentence
type: functional | non-functional | constraint
status: proposed                         # proposed | accepted | superseded | rejected
priority: medium                         # low | medium | high | critical
feature: [FEAT-###]                      # knowledge bridge
source: [<SRC-…>]                        # REQUIRED provenance
owners: [<name>]
acceptance: [<criterion>, <criterion>]   # how we know it's met
tags: [<tag>]
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
supersedes: []
superseded_by: []
relates_to: [DEC-###, ACT-###]
---

<Optional detail, rationale, or notes beyond `statement`.>
-->

## Open / Accepted Requirements

<!-- Place live items (proposed, accepted) here. -->

## Superseded / Rejected

<!-- Move items here when status changes. Keep them — do not delete. -->

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | <name> | Created file (counter=0). | Onboarding (<SRC-…>). |
