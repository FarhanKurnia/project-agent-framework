# Step 7 — Open Question Extraction

> Part of [Meeting Intelligence](README.md). Run after [Meeting Analysis](meeting-analysis.md), alongside the other extraction steps. **Often the most valuable step** — it captures what the project *doesn't* yet know.

## Purpose

Convert unresolved/ambiguous points from the analysis into formal `Q-###` items in `memory/open-questions.md`, each routed to whoever must answer it. This step also captures the questions raised by the *other* steps (unresolvable owner, unstated rationale, ambiguous scope).

## Inputs

- The in-session analysis (open-question candidates).
- Questions emitted by steps 4–6 (e.g., "who owns this action?", "why this decision?").
- `memory/open-questions.md` (current items + `counter`).

## Procedure

1. **Aggregate** all question candidates: those surfaced in the transcript, plus those raised during the other extraction steps.
2. **Load** existing open questions into a lookup.
3. **For each question**:
   1. **Search** for an existing question asking essentially the same thing.
      - Match → **update** (add context, append source, possibly raise `priority`), bump `updated`. Note reconciliation.
      - No match → **create** a new `Q-###` (increment `counter`) with `question`, `context`, `status: open`, `priority`, `needs_answer_from` (resolve to `ACTOR-###` where possible), `blocks` (link to `REQ/DEC/ACT` it holds up), `source: [<meeting_id>]`, dates.
   2. **Route** to an answerer: prefer the actor most likely to know (sponsor for scope, tech lead for architecture, business owner for policy). If unknown, set `needs_answer_from: [unresolved]` and flag for human triage.
   3. **Set `blocks:`** if the question is holding up a requirement or decision — this makes blocking questions visible at a glance.
4. **Close questions answered in this meeting**: if the transcript *resolved* an existing open question, set it `status: answered`, fill `answer`/`answered_by`/`answered_date`, and append the meeting to `source`. (The answer often spawns a new `DEC-###` or `REQ-###` — link it.)
5. **Record reconciliations** for the MOM.
6. **Write** the updated `memory/open-questions.md`.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/open-questions.md` | New/updated/answered `Q-###` items; counter updated. |
| Reconciliation notes | Fed into the MOM (including questions closed this meeting). |

## Rules

- **Prefer questions over guesses.** This is the framework's anti-hallucination valve. When steps 4–6 are unsure, they hand off here.
- **Provenance required.** `source: [<meeting_id>]`.
- **Every question has a target answerer** if one can be reasonably inferred; otherwise explicitly `unresolved`.
- **Answering is recorded, not deleted.** Closed questions stay with their answer — this builds the project's resolved-knowledge base.
- **Blocking questions are high-priority** by default; they gate requirements/decisions.

## Example

Candidate (from transcript): *"Not sure yet if contractors get portal access."* It blocks a scope decision.

No existing match → create `Q-002`:

```markdown
### Q-002 — Do contractors get portal access?

---
id: Q-002
title: Do contractors get portal access?
question: Are external contractors entitled to access the employee portal, and if so, with which permissions?
context: Determines Identity module scope and SSO entitlement rules. Raised during the kickoff.
status: open
priority: high
needs_answer_from: [ACTOR-002]
blocks: [REQ-001, DEC-001]
source: [SRC-MTG-2026-06-15]
answer:
answered_by:
answered_date:
created: 2026-06-15
updated: 2026-06-15
---
```

If a later meeting answers "Yes, read-only", set `Q-002.status: answered`, `answer: "Yes, read-only access."`, and likely create a `REQ` capturing the read-only contractor access rule — linked from `Q-002`.
