---
description: Build or import the backlog — derive from requirements, or ingest a raw backlog file
argument-hint: "[project-slug | raw-backlog-file]  e.g. hris  |  projects/hris/source/backlog/2026-06-20-roadmap.md"
---

# /backlog — Backlog Management

Build or groom the backlog for project **$ARGUMENTS** (default: infer project from cwd). Two modes: **INGEST** a raw backlog file, or **GENERATE** from accepted requirements.

## 1. Resolve mode + project
- If `$ARGUMENTS` resolves to an existing file (typically under `source/backlog/`) -> **INGEST mode**: run [Backlog Ingestion](../../capabilities/backlog-management/backlog-ingestion.md) on that raw backlog. `$PROJECT` is inferred from the file's path.
- Otherwise -> **GENERATE mode**: `$PROJECT` = first token if provided; if empty, infer from cwd (must be inside `projects/<slug>/`); if still unresolved, ask the user. Derive `BKL-###` from accepted requirements.

## 2. Read capability + sources
- Read `capabilities/backlog-management/`: INGEST -> `backlog-ingestion.md`; GENERATE -> `backlog-generation.md`. Then `prioritization.md`, `estimation-capture.md`, `dependency-mapping.md`, `grooming.md`. Plus `AGENTS.md`.
- Read `projects/$PROJECT/memory/requirements.md`, `knowledge/*` (FEAT/MOD), `memory/backlog.md`, `memory/open-questions.md`.

## 3. INGEST mode — parse + trace (Approach A)
- Parse the raw backlog into `BKL-###` work items; set `source: [<backlog_id>]`.
- Trace each item to `FEAT-###`/`MOD-###` and to an existing `REQ-###` where possible.
- **No dangling items:** an item tracing to no FEAT and no REQ -> propose a draft `REQ-###` (status: proposed) and link it, OR raise `Q-###`.
- Carry any priority/size/dependencies stated in the raw item. Surface embedded `DEC-###`/`Q-###`/`ASM-###`.
- If a raw item carries a tracker task id (e.g. `clickup:…`), set `external_ref`; its subtasks → the BKL `Subtasks:` checklist (manual two-way sync).

## 4. GENERATE mode — derive from accepted REQ
- Generate from REQ `status: accepted`.
- If only `proposed` exist: proceed but mark items `source-status: proposed` and remind the user the backlog is preliminary until REQs are accepted. Do not silently treat proposed as accepted.
- Decompose each REQ -> `BKL-###` (buildable, traced to REQ + FEAT).

## 5. Prioritize + estimate + dependencies (both modes)
- Priority (`priority`, MoSCoW / value-urgency), respecting REQ `phase`.
- Estimate (`estimate`); mark assumptions -> `ASM-###`.
- Dependencies (`blockedBy`); respect blocking Q.

## 6. Write output
- `projects/$PROJECT/memory/backlog.md` — increment counter, add/update BKL-###, preserve provenance.
- Any new `REQ-###`/`DEC-###`/`Q-###`/`ASM-###` -> their memory files.
- Don't overwrite old items -> supersede/link on change.

## 7. Guardrails
- Follow `AGENTS.md` (monotonic IDs, frontmatter, reconcile-before-add, supersede-never-delete).
- Provenance mandatory (`source:` on every item). No dangling backlog items.
- An estimate is an estimate (not a commitment).
- Ambiguity -> `Q-###`, don't guess. Data is private — don't commit/push.

## 8. Report briefly
- Mode used (INGEST/GENERATE); new BKL count + total backlog.
- Traceability: items linked to FEAT/REQ; draft REQ / Q raised for un-traced items.
- Priority order (top 5–10), critical dependencies, items blocked by Q-###.
