---
description: Onboard a new project (FSD-first) — build Knowledge from the FSD and initialize Memory
argument-hint: "<project-slug> [fsd-source]  e.g. hris  |  hris projects/hris/source/fsd"
---

# /onboard — Project Onboarding (FSD-first)

Onboard project **$ARGUMENTS** via the FSD-first path: two tracks — Knowledge from the FSD, and Memory initialized.

## 1. Resolve project and source
- First token = project slug (e.g. `hris`). If empty, ask for the slug and whether the FSD is already in place.
- Second token (optional) = FSD source directory (default `projects/<slug>/source/fsd/`).
- `$PROJECT` = that slug.

## 2. Scaffold (if not present)
- Create from `templates/`: `source/{fsd,brd,sop,meetings}/`, `knowledge/`, `memory/`, `outputs/`, plus a `project.md` manifest.
- Ensure the project is covered by the `.gitignore` rule `projects/*/` (private data — never commit/push).

## 3. Read and convert source
- Read `capabilities/meeting-intelligence/project-onboarding.md` + `AGENTS.md`.
- If FSD files are `.doc` MHTML (Confluence export) -> convert to text first (see note below). If `.docx`/`.pdf`/`.md` -> read directly.
- MHTML converter: a Python stdlib script (`email` + `html.parser` to parse multipart MHTML and strip HTML). Save output to `source/fsd/_txt/`.

## 4. Knowledge track (from the FSD)
Write to `projects/$PROJECT/knowledge/` (IDs per `AGENTS.md`):
- `project-overview.md`, `scope.md`, `actors.md` (ACTOR-###), `modules.md` (MOD-###),
  `features.md` (FEAT-###, mapped to MOD + ACTOR), `business-rules.md` (BR-###),
  `glossary.md` (term slugs).

## 5. Memory track (initialize)
Write to `projects/$PROJECT/memory/`:
- `requirements.md` (REQ-###, `status: proposed`, trace to FEAT, cite FSD section),
  `risks.md` (RSK-###), `assumptions.md` (ASM-###), `open-questions.md` (Q-### for ambiguity/gaps/image-only diagrams).
- Skeletons (counter 0): `decisions.md`, `action-items.md`, `backlog.md` (filled later from meetings/sprints).

## 6. Guardrails
- Follow `AGENTS.md` (ID system, frontmatter, provenance, reconcile-before-add, supersede-never-delete).
- Every Knowledge/Memory item MUST cite its FSD source (section).
- Ambiguity / missing info / image-only diagrams -> `Q-###`, do not guess.
- Update the `project.md` manifest (status: onboarded, changelog).

## 7. Report briefly
- Knowledge map (counts: FEAT/MOD/ACTOR/BR/glossary).
- Memory counts (REQ/RSK/ASM/Q).
- List of `Q-###` that need user input (by priority).
