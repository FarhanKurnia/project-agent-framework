---
doc_type: memory
memory_type: backlog
project: sample-helpdesk
last_reviewed: 2026-07-06
counter: 2
---

# Backlog — Acme Helpdesk (sample)

> Fictional sample. BKL-001 is committed to portfolio sprint `PS-01` (`sprint:` + `owner:` written by the portfolio commitment carve-out, `AGENTS.md` §7).

## New / Ready

### BKL-002 — SLA badge on ticket list

---
id: BKL-002
title: SLA badge on ticket list
description: Show an SLA breach/soon badge next to each ticket in the list view.
status: ready
priority: medium
size: S
confidence: medium
derived_from: [REQ-002]
delivers: [FEAT-002]
owner:
sprint: none
dependencies: []
source: [SRC-BKL-2026-06-20]
created: 2026-06-20
updated: 2026-06-20
---

## In Progress

### BKL-001 — Ticket import from email

---
id: BKL-001
title: Ticket import from email
description: Parse inbound support emails into tickets; dedupe by thread.
status: in-progress
priority: high
size: M
confidence: medium
derived_from: [REQ-001]
delivers: [FEAT-001]
skills_required: [backend, node]
owner: PERSON-002 (Ravi)
sprint: PS-01
dependencies: []
source: [SRC-BKL-2026-06-20]
created: 2026-06-20
updated: 2026-07-06
---

Committed to portfolio sprint `PS-01` (write-back on 2026-07-06: `sprint: PS-01`, `owner: PERSON-002 (Ravi)`, `status: in-progress`).

## Done / Dropped

*(none yet)*

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-20 | agent | Created BKL-001, BKL-002 (counter=2). | Portfolio sample. |
| 2026-07-06 | agent | BKL-001 → in-progress, sprint PS-01. | Portfolio Sprint Planning — commitment PS-01. |
