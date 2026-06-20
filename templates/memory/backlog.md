# Memory — Backlog (Template)

> Copy into `projects/<project>/memory/backlog.md`.
> **Backlog items** are units of work derived from accepted requirements/action items.
> Actively managed by the future Backlog Management capability (Phase 3).

---
doc_type: memory
memory_type: backlog
project: <project-slug>
last_reviewed: <YYYY-MM-DD>
counter: 0
---

# Backlog — <Project Name>

> Each backlog item is a `BKL-###`. Lifecycle: `new → ready → in-progress → done | dropped`.
> Trace each item to its origin (`REQ-###` / `ACT-###`) and its target `FEAT-###`.
> Optional: link to an execution tracker (e.g. ClickUp) via `external_ref`, and break work into a `Subtasks:` checklist (manual two-way sync).

<!-- TEMPLATE FOR A NEW ITEM:
### BKL-001 — <short title>

---
id: BKL-001
title: <short title>
description: <the work to be done, as a deliverable>
status: new                              # new | ready | in-progress | done | dropped
priority: medium                         # low | medium | high | critical
size: <t-shirt or points>                # S | M | L  or numeric estimate
confidence: <low | medium | high>
derived_from: [REQ-###, ACT-###]         # why this work exists
delivers: [FEAT-###]                     # what it builds
skills_required: [skill, …]              # OPTIONAL; if absent, portfolio skill-assignment infers from delivers/tags
owner: <name, ACTOR-###, or PERSON-###>
sprint: <sprint-id or none>            # per-project S-NN, or portfolio PS-NN (written by a portfolio sprint via the AGENTS.md §7 carve-out)
dependencies: [BKL-###]                  # blocking items
external_ref: <tracker task id>          # e.g. clickup:8612394 — link to execution tracker (two-way sync)
source: [<SRC-…>]                        # provenance
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---

<Optional detail / acceptance notes.>

Subtasks (optional — tracker task → subtask; manual two-way sync):
- [ ] <subtask>
- [x] <done subtask>
-->

## New / Ready

<!-- not yet scheduled -->

## In Progress

<!-- currently being worked -->

## Done / Dropped

<!-- retained for history -->

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | <name> | Created file (counter=0). | Onboarding (<SRC-…>). |
