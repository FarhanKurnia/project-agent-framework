# Step 1 — Project Onboarding (FSD-first)

> Part of [Meeting Intelligence](README.md). Run **once per new project**, before any per-meeting processing.
>
> **Key principle: the FSD (or equivalent authoritative product document) is the seed of Knowledge.**
> Meetings populate *Memory*; the FSD populates *Knowledge*. Onboarding seeds Knowledge from the FSD **first**, so that every subsequent meeting reconciles against a rich, accurate context.

## Purpose

Bootstrap a new project so that per-meeting processing has **Knowledge** (the stable picture of the product) and **Memory** (the living items) to reconcile against. Onboarding is split into two tracks:

- **Knowledge Track** — extracted **from the FSD** (and supplementary docs).
- **Memory Track** — populated **from meetings**, reconciled against the Knowledge Track.

## The two-track model

```
   KNOWLEDGE TRACK (FSD-driven)                  MEMORY TRACK (meeting-driven)
   ────────────────────────────                  ─────────────────────────────
   source/fsd/fsd-*.md  ──┐                      source/meetings/*.md ──┐
   source/brd, sop, …   ──┤                         (per meeting)        │
                          ▼                                              │
                   knowledge/*.md  ◀────── reconciled against ───────▶ memory/*.md
                   (actors, modules, features,                    (REQ/DEC/ACT/Q/RSK)
                    business-rules, glossary, scope)
```

The arrow that matters: **Memory extraction reads Knowledge first.** That is what prevents duplicates and wrong attributions ("the portal" → which module? → answer lives in `knowledge/modules.md`, seeded from the FSD).

## When to run

- A new project directory exists under `projects/` (with `templates/` copied in).
- At least the FSD has been filed under `source/fsd/`. *(If no FSD yet, see "No FSD yet" below.)*

## Inputs

- **`source/fsd/fsd-*.md`** — the authoritative product document (primary Knowledge source).
- Other available sources: `source/brd/`, `source/sop/`, any early `source/meetings/`.
- The `templates/` directory (already copied into the project).
- `AGENTS.md` (conventions).

## Procedure

### Phase A — Knowledge Track: seed from the FSD (do this FIRST)

1. **Read the FSD** end to end. It is the canonical description of the product.
2. **Write the manifest** `project.md`:
   - Fill name, slug, domain, phase, sponsor, tech lead, dates, summary, goals, non-goals from the FSD's purpose/background/scope sections.
   - Set the changelog: "Created. Onboarding (FSD: `<filename>`)".
3. **Populate Knowledge from the FSD:**
   - `knowledge/project-overview.md` — summary, goals, non-goals, context (from FSD §Purpose/§Background/§Scope).
   - `knowledge/actors.md` — extract every person/team/system the FSD names; assign `ACTOR-###`.
   - `knowledge/modules.md` — extract the functional building blocks; assign `MOD-###`.
   - `knowledge/features.md` — extract capabilities (often FSD §Functional Requirements / §User Flows); assign `FEAT-###`; map each to a module and actor.
   - `knowledge/business-rules.md` — extract constraints and policies (FSD §Non-Functional Requirements, §Assumptions); assign `BR-###`.
   - `knowledge/glossary.md` — seed domain terms by slug. This becomes the disambiguation hub.
   - `knowledge/scope.md` — derive phase in/out scope from the FSD's scope section.
4. **Mark every FSD-sourced entry** with its source filename in the Knowledge changelog/`Source:` field.
5. **Flag anything the FSD leaves ambiguous** (a module with no owner, an undefined term, an unstated non-functional target) — each becomes a `Q-###` in Phase C.

### Phase B — Knowledge Track: enrich from supplementary sources

6. **Read BRD/SOP/other docs** and **merge** into the existing Knowledge files (do not overwrite FSD-sourced facts; reconcile). Add new actors/modules/features/rules only where the supplementary doc extends the FSD. Note any **conflict** between FSD and BRD as a `Q-###` (do not silently pick one).

### Phase C — Memory Track: initialize and seed from explicit content

7. **Initialize** all six `memory/*.md` files from their templates (`counter: 0`), keeping template structure.
8. **Populate Memory ONLY from explicit source content** — never fabricate:
   - From the FSD's explicit **functional requirements**: create `REQ-###` (these are the product's stated needs — cite the FSD).
   - From any explicit **decisions/assumptions** stated as choices: create `DEC-###`.
   - From early meetings (if present): run the normal meeting extraction (steps 2–7 of Meeting Intelligence), reconciled against the now-rich Knowledge.
9. **Create one `Q-###` per ambiguous/missing item** identified in Phases A–B (e.g., "FSD does not specify the IdP vendor"). These seed the open-questions file and make onboarding gaps *visible*.
10. **Set memory counters** to the highest ID actually present in each file.

### Phase D — Report

11. **Report**: Knowledge created (counts per file), Memory initialized (counts), and the full list of `Q-###` open questions raised — these are the onboarding gaps a human should review.

## Outputs

| Artifact | Source | Notes |
|----------|--------|-------|
| `project.md` | FSD | Manifest — the project's identity. |
| `knowledge/*.md` | FSD (+ BRD/SOP) | First draft, conservatively populated; ambiguities flagged. |
| `memory/*.md` | explicit source content only | Skeletons + any directly-stated requirements/decisions; meetings fill the rest. |
| `memory/open-questions.md` | gaps found | At minimum one `Q-###` per FSD ambiguity. |

## Rules

- **FSD is canonical for Knowledge.** When the FSD and another source disagree about what the product *is*, the FSD wins for Knowledge; the disagreement becomes a `Q-###`.
- **Conservative extraction.** Err toward *less* Knowledge rather than wrong Knowledge. Inferences become open questions, not facts.
- **Cite sources.** Each Knowledge/Memory entry links to the source it came from (FSD filename or `SRC-MTG-…`).
- **No fabrication.** Never invent actors, modules, features, or rules the sources do not support.
- **Respect immutability.** Source files are read-only.
- **Counter integrity.** Each memory file's `counter` must equal its highest ID.

## No FSD yet

If there is **no FSD** at onboarding time:
- Fall back to the **most authoritative available document** (BRD > earliest meeting notes) as a *temporary* Knowledge seed.
- **Mandatory:** raise `Q-###` "FSD missing — Knowledge seeded from <fallback>; re-onboard when FSD lands."
- When the FSD arrives, re-run Phases A–B to **reconcile and upgrade** Knowledge (update, do not blindly overwrite — preserve any meeting-derived Memory and re-link it).

## Example

Input: `source/fsd/fsd-v1.0.md` describes an Employee Portal with an "Identity" module using corporate SSO, lists Employee/Finance/Corporate IdP as actors, and defines SSO as a functional requirement.

Phase A outputs:
- `knowledge/actors.md` → `ACTOR-001 Employee`, `ACTOR-T01 Finance`, `ACTOR-S01 Corporate IdP`.
- `knowledge/modules.md` → `MOD-001 Employee Portal`, `MOD-002 Identity`.
- `knowledge/features.md` → `FEAT-001 SSO Login` (→ `MOD-002`, serves `ACTOR-001`).
- `knowledge/glossary.md` → `sso`, `identity-provider`.
- `memory/requirements.md` → `REQ-001 SSO` (from the FSD's explicit functional requirement, `source: [fsd-v1.0.md]`).
- `memory/open-questions.md` → `Q-001 FSD does not name the IdP vendor — which one?` (ambiguity, NOT fabricated into Knowledge).

Result: when the kickoff meeting later says *"we'll use Okta"*, the extraction step resolves it to `MOD-002 Identity` / `FEAT-001` and creates `DEC-001 Okta`, **answering `Q-001`** — no duplicate module, no duplicate requirement.
