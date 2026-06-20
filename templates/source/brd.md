# BRD — Business Requirements Document (Template)

> Copy into `projects/<project>/source/brd/` as `brd-<period-or-version>.md`.
> **Source is immutable.** Once filed, do not edit — file a new version instead.

---
doc_type: brd
project: <project-slug>
version: <1.0>
date: <YYYY-MM-DD>
authors: [<name>]
status: draft | reviewed | approved | superseded
supersedes: []
business_owner: <name>
---

# Business Requirements Document — <Initiative Name>

## 1. Executive Summary
<One-paragraph overview of the business need and proposed outcome.>

## 2. Business Problem / Opportunity
<The current pain or opportunity. What happens if we do nothing?>

## 3. Business Objectives & Success Criteria
<Objectives and how success is measured (KPIs). Each objective may drive `REQ-###`.>

| Objective | Metric / KPI | Target |
|-----------|--------------|--------|
| <…> | <…> | <…> |

## 4. Background & Strategic Fit
<How this aligns with broader strategy. Related decisions (`DEC-###`).>

## 5. Stakeholders
<Sponsors, business owners, impacted teams. Cross-link to `knowledge/actors.md`.>

## 6. Current State
<How things work today.>

## 7. Proposed / Future State
<How things should work. Capabilities at a high level.>

## 8. Business Requirements
<What the business needs (the "what", not the "how"). Each may become a `REQ-###`.>

1. <BR-001 …>
2. <BR-002 …>

## 9. Scope
**In scope:** …
**Out of scope:** …
<Reconcile with `knowledge/scope.md`.>

## 10. Assumptions, Dependencies & Constraints
<Candidates for `memory/open-questions.md` / `memory/risks.md`.>

## 11. Risks
<Known business risks. May seed `memory/risks.md` (`RSK-###`).>

## 12. High-Level Timeline / Milestones
<Major phases and dates.>

## 13. Glossary
<Terms. Reconcile into `knowledge/glossary.md`.>

## 14. References
<Related FSDs, SOPs, meetings.>
