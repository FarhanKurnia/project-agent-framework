---
description: Portfolio sprint planning — propose a cross-project sprint (PS-NN); commitment needs human approval
argument-hint: "[slug slug ...]  e.g. hris crm  (default: read portfolio/manifest.md)"
---

# /portfolio — Portfolio Sprint Planning

Plan a **portfolio sprint** (`PS-NN`) that spans multiple projects. **Commitment requires human approval** — this command PROPOSES a cross-project sprint; it does not write back to projects without the user's OK.

## 1. Resolve in-scope projects
- `$PROJECTS` = the slugs in `$ARGUMENTS` if provided; otherwise read `portfolio/manifest.md` ("In-scope projects"); if empty/ambiguous, ask the user. No hardcoded default.

## 2. Read capability and sources
- Read `capabilities/portfolio-sprint-planning/`: `portfolio-capacity-modeling.md`, `portfolio-sprint-proposal.md`, `portfolio-sprint-commitment.md`, `portfolio-sprint-review-prep.md`. Plus `AGENTS.md` (esp. §3 qualified refs + §7 write-back carve-out).
- Read `portfolio/manifest.md` (sprint counter → next `PS-NN`).
- For each in-scope slug: read `projects/<slug>/memory/backlog.md` (BKL) and `knowledge/actors.md` / `memory/assumptions.md` for contributors.

## 3. Model pooled capacity
- Pool contributors across in-scope projects; sum available time; apply focus factor.
- No portfolio velocity yet → ideal-days, flagged as an estimate. Record `ASM-###` per project where relevant.

## 4. Propose the sprint (PROPOSE, not COMMIT)
- Collect each project's `ready` BKLs, rewrite every ref as `<slug>:BKL-###`.
- Order by priority + dependencies (incl. cross-project) + size; fill the pooled budget.
- Draft a cross-project goal; list carry-forward candidates + exclusions (with reasons; low-readiness → `Q-###`).

## 5. Write output (as a PROPOSAL)
- `portfolio/sprints/sprint-PS-NN-<window-start>.md` from `templates/outputs/portfolio-sprint.md` — mark `status: proposed`.
- Bump `sprint_counter` in `portfolio/manifest.md`.
- Do NOT write to any project's backlog yet — write-back happens only at commitment.

## 6. Guardrails
- Follow `AGENTS.md`. Qualified refs (`<slug>:BKL-###`) everywhere — never bare `BKL-###`.
- Commitment is a human-approved step with a narrow write-back carve-out (§7): only `sprint:` + `owner:` (+ `status: in-progress`, `updated`) into each project's `memory/backlog.md`.
- Real portfolio data is gitignored/private — do not commit/push.

## 7. Report briefly and ask for approval
- Sprint `PS-NN`, pooled capacity vs estimate, selected `<slug>:BKL-###` items, dependencies/risks.
- Ask: *"Approve this portfolio sprint to commit (write-back to each project), or revise first?"* → only commit if approved.
