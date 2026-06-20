# Capability — Meeting Intelligence

> **Status:** 🟦 Specified — ready for any LLM agent to execute.
> The first and currently specified capability of `project-agent-framework`.

## Purpose

Turn raw meeting transcripts (`source/meetings/*`) into **structured Minutes of Meeting** and **reconciled memory** (requirements, decisions, action items, open questions) — without duplicating what the project already knows.

Meeting Intelligence is what makes a new project *useful*: **onboarding seeds Knowledge from the FSD first**, the first meeting bootstraps Memory against that Knowledge, and every subsequent meeting *reconciles* instead of rebuilding from scratch.

## The pipeline

A meeting flows through these steps. Onboarding is run once per project; the rest run per meeting.

```
                    (once per project)
   ┌──────────────────────────────────┐
   │  1. Project Onboarding (FSD-first)│  FSD → knowledge/ (seed) + memory/ skeleton + project.md
   └──────────────────────────────────┘
                    │
   ┌──────────────────────────────────┐
   │  (per meeting)                    │
   │  2. Meeting Analysis              │  transcript → structured understanding
   └──────────────────────────────────┘
                    │
          ┌─────────┴──────────┐
          ▼                    ▼
   ┌──────────────┐   ┌──────────────────────────────────────┐
   │ 3. MOM Gen   │   │  Extraction (run all four, then       │
   │  → outputs/  │   │  reconcile together):                 │
   └──────────────┘   │   4. Requirements  → memory/req.md     │
                      │   5. Decisions      → memory/dec.md    │
                      │   6. Action Items   → memory/act.md    │
                      │   7. Open Questions → memory/q.md      │
                      └──────────────────────────────────────┘
```

> **Order matters within a meeting run:** analyze → generate MOM → extract (all four) → reconcile. The extraction steps share the same analysis and must reconcile against *existing* memory before writing.

## Inputs & outputs at a glance

| Step | Reads | Writes |
|------|-------|--------|
| 1. Project Onboarding | **FSD** (primary) + BRD/SOP + early meetings | `project.md`, `knowledge/*` (seeded from FSD), `memory/*` (skeleton) |
| 2. Meeting Analysis | `source/meetings/<file>`, `knowledge/*` | (in-session structured understanding — feeds 3–7) |
| 3. MOM Generation | analysis from step 2 | `outputs/meetings/*-mom.md` |
| 4. Requirement Extraction | analysis + `memory/requirements.md` + `knowledge/features.md` | `memory/requirements.md` |
| 5. Decision Extraction | analysis + `memory/decisions.md` | `memory/decisions.md` |
| 6. Action Item Extraction | analysis + `memory/action-items.md` + `knowledge/actors.md` | `memory/action-items.md` |
| 7. Open Question Extraction | analysis + `memory/open-questions.md` | `memory/open-questions.md` |

## Cross-cutting rules (apply to every step)

1. **Provenance is mandatory.** Every memory item created in steps 4–7 must set `source: [<meeting_id>]` (the `meeting_id` from the source file's frontmatter).
2. **Reconcile before you write.** For each candidate item, search existing memory for a match. Update in place rather than duplicating. Record reconciliations in the MOM's *Reconciliations* section.
3. **Respect the ID counter.** Each memory file tracks its `counter`. Increment it for every new item; never reuse an ID.
4. **Link liberally.** New requirements link to features (`FEAT-###`) and decisions (`DEC-###`); action items link to owners (`ACTOR-###`) and their driving decision.
5. **Never invent.** If the transcript is ambiguous, raise a `Q-###` instead of guessing a requirement/decision.
6. **One project only.** Confine all writes to the target project's directories. See `AGENTS.md` §7.
7. **Follow `AGENTS.md`.** ID conventions, frontmatter shapes, and the editing disciplines are defined there and in `templates/`.

## Step specifications

Each step has its own file with inputs, procedure, outputs, rules, and an example:

1. [`project-onboarding.md`](project-onboarding.md)
2. [`meeting-analysis.md`](meeting-analysis.md)
3. [`mom-generation.md`](mom-generation.md)
4. [`requirement-extraction.md`](requirement-extraction.md)
5. [`decision-extraction.md`](decision-extraction.md)
6. [`action-item-extraction.md`](action-item-extraction.md)
7. [`open-question-extraction.md`](open-question-extraction.md)

## How an agent runs this

> *"Process `projects/hris/source/meetings/2026-06-15-standup.md`."*

1. Read `AGENTS.md`, this `README.md`, and the source file.
2. Resolve the target project (`hris`) and read its current `knowledge/*` and `memory/*`.
3. Run **Meeting Analysis** (step 2) in-session.
4. Run **MOM Generation** (step 3) → write the MOM.
5. Run the four **Extraction** steps (4–7), reconciling against existing memory.
6. Update the relevant `memory/*` files and the MOM's reconciliation section.
7. Report: items created, items updated/reconciled, and anything flagged for human review.

## Definition of done

- [x] All seven steps specified as executable procedures.
- [x] MOM + memory templates available in `templates/`.
- [x] `sample-project/` demonstrates a full end-to-end run on a fictional meeting.
