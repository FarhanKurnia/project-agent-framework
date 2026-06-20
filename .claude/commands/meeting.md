---
description: Process a meeting (Meeting Intelligence) — analysis to MOM to extract REQ/DEC/ACT/Q, reconciled to Knowledge
argument-hint: "<file-or-date>  e.g. 2026-06-25  |  projects/<project-slug>/source/meetings/2026-06-25-kickoff.md"
---

# /meeting — run Meeting Intelligence

Process meeting **$ARGUMENTS** with the **Meeting Intelligence** capability, then write the results to the relevant project.

## 1. Resolve the meeting source
- If `$ARGUMENTS` is empty -> list files in `projects/*/source/meetings/`, then ask the user which one to process.
- If it is a date (e.g. `2026-06-25`) -> find the matching file under `projects/*/source/meetings/`.
- If it is a path -> use that path.
- **Project** (`$PROJECT`) is inferred from the meeting path (e.g. `projects/<slug>/...` -> project `<slug>`); if only a date is given, infer from cwd (must be inside `projects/<slug>/`), or ask the user.
- Read the raw notes in full.

## 2. Follow the capability docs (read as needed)
- `capabilities/meeting-intelligence/meeting-analysis.md`
- `capabilities/meeting-intelligence/mom-generation.md`
- `capabilities/meeting-intelligence/requirement-extraction.md`
- `capabilities/meeting-intelligence/decision-extraction.md`
- `capabilities/meeting-intelligence/action-item-extraction.md`
- `capabilities/meeting-intelligence/open-question-extraction.md`
- Honor the universal contract `AGENTS.md` (ID system, frontmatter, mandatory provenance, reconcile-before-add, supersede-never-delete).

## 3. Reconcile against existing Knowledge and Memory
- Read `projects/$PROJECT/knowledge/*` and `projects/$PROJECT/memory/*`.
- Map attendee names -> `ACTOR-###`, terms -> glossary, features -> `FEAT-###/MOD-###`.
- Do not duplicate existing items -> link (`relates_to`) or supersede on change.
- Ambiguity / missing info -> raise `Q-###`, **do not guess**.

## 4. Write outputs (increment counters, cite provenance)
Every extracted item MUST cite `source: [<meeting_id>]` from the meeting frontmatter.
- `projects/$PROJECT/outputs/mom/<meeting_id>.md` — Minutes of Meeting.
- append to `projects/$PROJECT/memory/`:
  - `requirements.md` (new REQ-### if new needs arise)
  - `decisions.md` (DEC-###)
  - `action-items.md` (ACT-###)
  - `open-questions.md` (Q-###)

## 5. Report briefly
- What was extracted (count of new REQ/DEC/ACT/Q).
- Which are new vs reconciled/linked to existing items.
- New `Q-###` that need the user's answer.
- Confirm which files were written.

## Guardrails
- Cite a source, reconcile before adding, raise Q-### over assuming.
- Source (raw notes) is immutable — do not edit it; corrections go in a follow-up note/meeting.
- Project data under `projects/*/` is private — never commit/push.
