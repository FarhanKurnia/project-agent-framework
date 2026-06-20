# Step 2 — Prioritization

> Part of [Backlog Management](README.md). Run after [Backlog Generation](backlog-generation.md).

## Purpose

Assign a **priority** to each backlog item using a stated method, and **record the rationale as a decision** (`DEC-###`) so the priority is defensible and changeable later.

## Inputs

- `memory/backlog.md` — items at `status: new | ready`.
- `memory/decisions.md` — to record prioritization rationale.
- `memory/requirements.md` — requirement `priority` as an input signal.
- `knowledge/scope.md` — phase goals to align priority against.

## Procedure

1. **Choose a method** for this run (state it explicitly in the decision). Two supported:
   - **MoSCoW** — Must / Should / Could / Won't (this phase).
   - **Value vs. Effort** — high-value/low-effort first; map to `priority: critical|high|medium|low`.
2. **Score each item**, drawing on:
   - The originating `REQ-###` priority.
   - Whether it unblocks other items (see step 4) or enables a phase goal (`knowledge/scope.md`).
   - Stated deadlines (e.g., a "live by July" requirement raises its items).
3. **Set `priority`** on the backlog item (`low | medium | high | critical`).
4. **Record the rationale** as one `DEC-###` per prioritization run (batch), capturing: the method used, the key drivers, and any notable calls (e.g., "BKL-003 deprioritized because its requirement is phase 2"). Link `affects: [BKL-…]`.
5. **Flag contentious calls.** If two stakeholders would likely disagree on a priority, raise a `Q-###` and mark the priority as provisional.

## Outputs

| Artifact | Notes |
|----------|-------|
| `memory/backlog.md` | `priority` set on each item. |
| `memory/decisions.md` | One `DEC-###` documenting the prioritization method + rationale. |
| `memory/open-questions.md` | `Q-###` for any contentious/provisional priority. |

## Rules

- **Method must be explicit.** "Gut feel" is not allowed — name MoSCoW or Value/Effort and apply it consistently.
- **Rationale is a decision.** Priorities change; the *why* must survive in `DEC-###` so a future change is reasoned, not arbitrary.
- **Provenance required** on the `DEC-###`.
- **Never silently reorder.** Changing a priority later = a new `DEC-###` that supersedes the prior rationale.

## Example

Run: MoSCoW against Phase-1 scope. `BKL-001` (Okta SSO) is on the critical path for the July pilot → `priority: critical`. `BKL-003` (contractor access) depends on an unresolved `Q-002` → `priority: low` (provisional).

Record `DEC-002`:

```markdown
### DEC-002 — Backlog prioritization (MoSCoW, Phase 1)

---
id: DEC-002
title: Backlog prioritization (MoSCoW, Phase 1)
status: accepted
context: Initial backlog needs ordering for Phase-1 delivery toward the July pilot and August go-live.
decision: Apply MoSCoW; mark SSO-critical-path items Must/Critical, defer contractor-access items pending Q-002.
rationale: SSO is the gating dependency for pilot onboarding (REQ-001, DEC-001); contractor scope is unresolved (Q-002).
consequences: BKL-001 critical; BKL-003 low (provisional).
scope: project-wide
source: [SRC-MTG-2026-06-15]
deciders: [ACTOR-001]
affects: [BKL-001, BKL-003]
...
---
```
