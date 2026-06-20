---
doc_type: memory
memory_type: backlog
project: sample-intranet
last_reviewed: 2026-07-06
counter: 2
---

# Backlog — Acme Intranet (sample)

> Fictional sample. BKL-001 is committed to portfolio sprint `PS-01`. BKL-002 is `new`/low-confidence — excluded from PS-01 (carry-forward candidate).

## New / Ready

### BKL-002 — Announcement editor (rich text)

---
id: BKL-002
title: Announcement editor (rich text)
description: Rich-text editor for composing intranet announcements with image embeds.
status: new
priority: low
size: L
confidence: low
derived_from: [REQ-002]
delivers: [FEAT-002]
owner:
sprint: none
dependencies: []
source: [SRC-BKL-2026-06-20]
created: 2026-06-20
updated: 2026-06-20
---

Not in PS-01: fails the readiness gate (`confidence: low`, not yet sized firmly). Carry-forward to a later portfolio sprint.

## In Progress

### BKL-001 — SSO integration (intranet)

---
id: BKL-001
title: SSO integration (intranet)
description: Integrate the intranet with the corporate identity provider for single sign-on.
status: in-progress
priority: high
size: M
confidence: medium
derived_from: [REQ-001]
delivers: [FEAT-001]
skills_required: [backend, sso]
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
