---
description: Sprint planning — capacity to proposal (commitment needs human approval)
argument-hint: "[project-slug]  e.g. hris  (default: infer from cwd)"
---

# /sprint — Sprint Planning

Plan a sprint for project **$ARGUMENTS** (default: infer from cwd). **Sprint commitment requires human approval** — this command PROPOSES; it does not finalize without the user's OK.

## 1. Resolve project
- `$PROJECT` = first token if provided; if empty, infer from cwd (must be inside `projects/<slug>/`); if still unresolved, ask the user. No hardcoded default.

## 2. Read capability and sources
- Read `capabilities/sprint-planning/`: `capacity-modeling.md`, `sprint-proposal.md`, `sprint-commitment.md`, `sprint-review-prep.md`. Plus `AGENTS.md`.
- Read `projects/$PROJECT/memory/backlog.md` (BKL), `requirements.md` (phase/priority), `risks.md`, `open-questions.md`.

## 3. Model capacity
- Capacity = team, velocity (history/estimate), availability, sprint working days.
- If team/velocity data is missing -> ask the user or use a clearly stated assumption (record `ASM-###`).

## 4. Propose the sprint (PROPOSE, not COMMIT)
- Pull BKLs from the backlog in priority order + respect dependencies (blockedBy) + fit capacity.
- Respect `phase` and blocking Q (e.g. phasing not yet final).
- Result: list of BKLs in the sprint + total estimate vs capacity + risks/blockers.

## 5. Write output (as a PROPOSAL)
- `projects/$PROJECT/outputs/sprint-<id>.md` — mark `status: proposed`.
- Do NOT flip BKL `status` to "committed" / do not finalize commitment without explicit user approval.

## 6. Guardrails
- Follow `AGENTS.md`.
- Sprint-commitment is a human-approved step: only after the user OKs it, run commitment (set BKL status, write the final sprint).
- Assumptions -> `ASM-###`. Ambiguity -> `Q-###`. Data is private — do not commit/push.

## 7. Report briefly and ask for approval
- Sprint ID, capacity vs estimate filled, selected BKLs, dependencies/risks.
- Ask: *"Approve this sprint to commit, or revise first?"* -> only commit if approved.
