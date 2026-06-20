---
description: Turn requirements into a backlog (priority + estimation + dependencies)
argument-hint: "[project-slug]  e.g. hris  (default: infer from cwd)"
---

# /backlog — Backlog Management

Build or groom the backlog for project **$ARGUMENTS** (default: infer from cwd): turn requirements into ordered work items.

## 1. Resolve project
- `$PROJECT` = first token if provided; if empty, infer from cwd (must be inside `projects/<slug>/`); if still unresolved, ask the user. No hardcoded default.

## 2. Read capability and sources
- Read `capabilities/backlog-management/`: `backlog-generation.md`, `prioritization.md`, `estimation-capture.md`, `dependency-mapping.md`, `grooming.md`. Plus `AGENTS.md`.
- Read `projects/$PROJECT/memory/requirements.md`, `knowledge/*` (FEAT/MOD), `memory/open-questions.md` (blocking Q).

## 3. Governance: REQ must be accepted
- The backlog is generated from REQ with `status: accepted`.
- If only `proposed` exist (not yet signed off): proceed but clearly mark every item `source-status: proposed` and remind the user the backlog is preliminary until REQs are accepted. Do not silently treat proposed as accepted.

## 4. Generate BKL items
- Decompose each REQ -> `BKL-###` buildable work item, traced to `REQ-###` and `FEAT-###`.
- Priority: `priority` field (MoSCoW / value-urgency). Respect REQ `phase` (phasing determines order).
- Estimation: `estimate` (story points / effort / size) — based on FEAT and related BR complexity.
- Dependencies: `blockedBy: [BKL-###]` and `relates_to`; respect blocking Q.

## 5. Write output
- `projects/$PROJECT/memory/backlog.md` — increment counter, add BKL-###, preserve provenance fields.
- Do not overwrite old items -> supersede/link on change.

## 6. Guardrails
- Follow `AGENTS.md` (monotonic IDs, frontmatter, reconcile-before-add, supersede-never-delete).
- An estimate is an estimate (not a commitment); mark assumptions -> `ASM-###`.
- Ambiguity -> `Q-###`, do not guess. Data is private — do not commit/push.

## 7. Report briefly
- New BKL count and total backlog.
- Priority order (top 5–10), critical dependencies, items blocked by Q-###.
- Governance note (proposed vs accepted).
