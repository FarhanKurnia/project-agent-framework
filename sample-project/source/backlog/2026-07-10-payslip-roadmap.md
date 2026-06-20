---
doc_type: raw-backlog
project: sample-employee-portal
backlog_id: SRC-BKL-2026-07-10
title: Payslip Viewer roadmap (draft)
date: 2026-07-10
origin: Product planning dump (from the PM's ClickUp list)
author: PM (Acme)
status: raw
---

# Payslip Viewer roadmap (draft) — 2026-07-10

> ⚠️ Fictional sample. Raw backlog feeding **Backlog Ingestion (Step 1b)**. FEAT-002 (Payslip Viewer) has no formal requirement yet, so ingestion proposes a draft `REQ-002` and links these items to it. This file holds **multiple tasks** (not one task per file).

## 1. Context / objective
Pick up the Payslip Viewer (FEAT-002) once the SSO pilot is stable. Two chunks of work needed before the August demo.

## 2. Items

### Payslip Viewer
- [ ] Build payslip viewer (current + historical)   `clickup:8612394`
    - [ ] fetch payslips from payroll API
    - [ ] list view + detail view
    - [ ] handle empty state
- [ ] Add payslip PDF export                         `clickup:8612395`
    - [ ] PDF rendering
    - [ ] download button

## 3. Priorities mentioned
Viewer before export. Both needed before the August demo.

## 4. Dependencies / order mentioned
PDF export depends on the viewer existing.

## 5. Assumptions / decisions embedded
The payroll API already exists (assumption).

## 6. Open questions / unknowns
Does the payroll API expose historical payslips older than 12 months?

---
<!-- Notes for the agent: -->
<!-- - Ingest with /backlog. Both items trace to FEAT-002 (Payslip Viewer). -->
<!-- - FEAT-002 has no REQ -> propose draft REQ-002 (proposed) and link. -->
<!-- - clickup ids -> external_ref; nested bullets -> Subtasks checklist. -->
