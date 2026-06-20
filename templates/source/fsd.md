# FSD — Functional Specification Document (Template)

> Copy into `projects/<project>/source/fsd/` as `fsd-v<major>.<minor>.md`.
> **Source is immutable.** Once filed, do not edit — file a new version instead.

---
doc_type: fsd
project: <project-slug>
version: <1.0>
date: <YYYY-MM-DD>
authors: [<name>]
status: draft | reviewed | approved | superseded
supersedes: []               # prior FSD version filenames, if any
---

# Functional Specification Document — <Project / Module Name>

## 1. Purpose
<What this document specifies and why it exists.>

## 2. Scope
<What is in and out of scope for this specification. Cross-link to `knowledge/scope.md`.>

## 3. Background & Context
<Relevant history, prior decisions, related systems.>

## 4. Stakeholders & Actors
<List the people, teams, and systems involved. Cross-link to `knowledge/actors.md`.>

## 5. Functional Requirements
<Numbered list of what the system must do. Each may become a `REQ-###` in memory.>

1. <FR-001 …>
2. <FR-002 …>

## 6. User Flows / Use Cases
<Step-by-step descriptions or scenarios.>

### 6.1 <Use case name>
**Actor:** <ACTOR-###>
**Preconditions:** …
**Main flow:** …
**Postconditions:** …

## 7. Data & Interfaces
<Data models, inputs/outputs, integrations. High-level only; reference a data dictionary if needed.>

## 8. Non-Functional Requirements
<Performance, security, availability, compliance. Each may become a `REQ-###`.>

## 9. Assumptions & Dependencies
<What must be true for this spec to hold. Candidates for `memory/open-questions.md` or a future `memory/assumptions.md`.>

## 10. Open Issues
<Unresolved items — strong candidates for `memory/open-questions.md` (`Q-###`).>

## 11. Glossary
<Terms used. Should be reconciled into `knowledge/glossary.md`.>

## 12. References
<Related BRDs, SOPs, meetings. Use filenames.>
