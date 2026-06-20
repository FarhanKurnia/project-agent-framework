# Capability — Profile Management

> **Status:** 🟦 Specified — ready for any LLM agent to execute.
> Phase 6b capability of `project-agent-framework`. Maintains the **build-team roster** (`portfolio/profiles/team.md`) — the `PERSON-###` personas that power skill-based assignment and effective-sprint planning.

## Purpose

Keep the org-wide build-team profile trustworthy: onboard real people (with provenance), maintain skills/availability over time, supersede (never delete), and reconcile each person's `current_load` from in-flight portfolio sprints — so Portfolio Sprint Planning can recommend owners by skill and capacity.

## Where it lives
- **Roster:** `portfolio/profiles/team.md` (gitignored — real people data).
- **Template:** [`templates/portfolio/team.md`](../../templates/portfolio/team.md).
- **IDs:** `PERSON-###` (persons), optional `TEAM-###` (squads) — org-wide, distinct from per-project `ACTOR-###`.
- **Command:** `/profile`.

## Relationship to other capabilities
- Feeds **[Portfolio Sprint Planning](../portfolio-sprint-planning/README.md)** — per-person capacity ceiling, skill-based owner assignment, coverage matrix.
- `current_load` is recomputed from committed portfolio sprints (`portfolio/sprints/*` at `status: committed`).

## The pipeline (sub-workflows)
```
 HR / hiring record ──▶ 1. Onboard        → new PERSON-### (reconcile by name/email)
 team change        ──▶ 2. Maintain        → edit skills/level/availability; supersede → alumni
 (any sprint change)──▶ 3. Reconcile load  → recompute current_load from in-flight sprints
```

## Inputs & outputs
| Step | Reads | Writes |
|------|-------|--------|
| Onboard | HR/hiring source, existing `team.md` | new `PERSON-###` in `team.md` |
| Maintain | `team.md`, change source | edited `PERSON-###` (+ changelog) |
| Reconcile load | `portfolio/sprints/*` (committed) | `current_load:` on each PERSON |

## Cross-cutting rules
1. **Provenance required.** Every `PERSON-###` cites a source (HR roster, hiring record). No uncited personas.
2. **Reconcile before add.** Search for an existing person by name/email before creating a `PERSON-###`.
3. **Supersede, never delete.** A person leaving → `status: alumni` (keep history; ID never reused).
4. **`PERSON-###` ≠ `ACTOR-###`.** Persons *build*; actors are *system users*. Link, don't merge.
5. **`current_load` is derived**, not hand-set — recomputed by load-reconciliation.
6. **Confidential.** `team.md` is gitignored; never commit real people data.

## Step specifications
1. [`profile-onboarding.md`](profile-onboarding.md)
2. [`profile-maintenance.md`](profile-maintenance.md)
3. [`load-reconciliation.md`](load-reconciliation.md)

## How an agent runs this
> *"`/profile add` — onboard Ravi, senior backend, [node, postgres], 100%, home helpdesk."* or *"`/profile load`."*

1. Read this `README.md` + the relevant step + `AGENTS.md`.
2. Execute the step on `portfolio/profiles/team.md` (reconcile before add).
3. Report the new/updated `PERSON-###`.

## Definition of done
- [x] All three sub-workflows specified.
- [x] Profile template: `templates/portfolio/team.md`.
- [x] `PERSON-###`/`TEAM-###` convention in `AGENTS.md` §3.
