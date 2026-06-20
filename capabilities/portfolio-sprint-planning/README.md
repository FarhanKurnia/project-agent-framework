# Capability — Portfolio Sprint Planning

> **Status:** 🟦 Specified — ready for any LLM agent to execute.
> Phase 6a capability of `project-agent-framework`. The **cross-project** counterpart to [Sprint Planning](../sprint-planning/README.md): turns the ready backlog of *multiple* projects into one committed, time-boxed **portfolio sprint**.

## Purpose

Given the ready backlogs of several `projects/<slug>/` and a pooled team capacity, propose a **single sprint that spans multiple projects**, record the committed scope (with qualified `<slug>:BKL-###` refs), and write the assignment back into each project's backlog. This is how the framework plans work when one team builds more than one application.

## Where it lives

- **Artifacts:** `portfolio/sprints/sprint-<PS-NN>-<date>.md` (cross-project, repo root — see [`portfolio/README.md`](../../portfolio/README.md)).
- **IDs:** `PS-NN` (portfolio sprint, org-wide; counter in [`portfolio/manifest.md`](../../portfolio/manifest.md)).
- **Refs:** every backlog item is referenced as `<slug>:BKL-###`.

## Relationship to per-project Sprint Planning

This capability **reuses** the per-project [Sprint Planning](../sprint-planning/README.md) steps by reference — capacity modeling, proposal, commitment, review — and extends them for the cross-project case. The per-project capability is **unchanged**; single-project teams keep using `S-NN` sprints under `projects/<slug>/outputs/sprints/`.

## The one new rule: the write-back carve-out

Committing a portfolio sprint is the **second** sanctioned exception to "do not cross projects" (the first is Reporting's read-only synthesis). On human approval, the Commitment step may write **only** `sprint:` (`PS-NN`) and `owner:` (plus bump `status: in-progress`, `updated`) into each referenced project's `memory/backlog.md` — for exactly the `<slug>:BKL-###` items in the committed scope. Nothing else. See [`AGENTS.md`](../../AGENTS.md) §7.

## The pipeline

Steps 1–3 run at **sprint start**; step 4 at **sprint end**.

```
 in-scope projects (slugs) + pooled team ─┐
                                          ├─ 1. Capacity Modeling   → pooled budget (per-person ceiling in Phase B)
 ready BKL-### across those projects ─────┤
                                          ├─ 2. Sprint Proposal      → recommended cross-project set (qualified refs)
                                          ├─ 3. Sprint Commitment     → committed scope; write-back to each project's backlog
                                          │
 (sprint end)                             └─ 4. Sprint Review Prep    → per-project done/partial; carry-overs
```

## Inputs & outputs at a glance

| Step | Reads | Writes |
|------|-------|--------|
| 1. Capacity | each in-scope `knowledge/actors.md` (or manifest), window, holidays, prior `portfolio/sprints/*` velocity | capacity budget (in the sprint artifact) |
| 2. Proposal | each in-scope `memory/backlog.md` (`ready`), capacity from step 1, `portfolio/manifest.md` | `portfolio/sprints/sprint-<PS-NN>-<date>.md` (proposed); `manifest.md` counter bumped |
| 3. Commitment | proposed sprint + human approval | sprint artifact (committed); each project's `memory/backlog.md` (`sprint:`, `owner:`, `status: in-progress`) |
| 4. Review | committed sprint, each project's backlog status | sprint artifact review section (closed); each project's backlog (close done) |

## Cross-cutting rules

1. **Propose, then commit.** Proposal = agent recommendation; commitment = human approval. Never auto-commit.
2. **Qualified refs everywhere.** Always `<slug>:BKL-###`. Never bare `BKL-###` in a portfolio artifact.
3. **Respect dependencies** — including cross-project ones (a `<slug2>:BKL-###` blocking a `<slug1>:BKL-###`). A blocked item whose blocker is not in-scope (or already delivered) is deferred.
4. **Respect capacity.** Pooled budget is a ceiling. (Phase B enforces a per-person ceiling.)
5. **Sprint-readiness gate.** Only `ready` items (sized, `confidence ≥ medium`) are eligible; others are carry-forward candidates or `Q-###`.
6. **The write-back carve-out.** Commitment writes only `sprint:` + `owner:` to projects (see above + `AGENTS.md` §7). Bidirectional integrity is mandatory.
7. **Never delete — transition.** Scope changes by status transitions.
8. **Follow `AGENTS.md`.** ID conventions, frontmatter, editing disciplines.

## Step specifications

1. [`portfolio-capacity-modeling.md`](portfolio-capacity-modeling.md)
2. [`portfolio-sprint-proposal.md`](portfolio-sprint-proposal.md)
   - 2b. [`skill-assignment.md`](skill-assignment.md) — recommend `PERSON-###` owners + render the coverage matrix
3. [`portfolio-sprint-commitment.md`](portfolio-sprint-commitment.md)
4. [`portfolio-sprint-review-prep.md`](portfolio-sprint-review-prep.md)

## How an agent runs this

> *"Propose the next portfolio sprint for `sample-employee-portal` + `sample-helpdesk`, window 2026-07-06 to 2026-07-19."*

1. Read `AGENTS.md`, this `README.md`, [`portfolio/manifest.md`](../../portfolio/manifest.md), and each in-scope project's `memory/backlog.md` + `knowledge/actors.md`.
2. Run **Capacity Modeling** (step 1) → pooled budget.
3. Run **Sprint Proposal** (step 2) → recommend a cross-project set; write `portfolio/sprints/sprint-<PS-NN>-<date>.md` (status: proposed). Increment `sprint_counter` in `manifest.md`.
4. **Stop for human approval.** On approval, run **Commitment** (step 3) → write-back to each project's backlog.
5. At sprint end, run **Review Prep** (step 4) → record outcomes per project.

> **Skill-based assignment (profiles):** step 1 enforces a per-person capacity ceiling from `portfolio/profiles/team.md`; step 2b ([`skill-assignment.md`](skill-assignment.md)) recommends `PERSON-###` owners by skill-overlap, renders a coverage matrix, and raises `Q-###` for skill gaps. If no roster exists, owners are free-text. Maintain the roster via [Profile Management](../profile-management/README.md) (`/profile`).

## Definition of done

- [x] All four steps specified as executable procedures.
- [x] Portfolio sprint artifact template: [`templates/outputs/portfolio-sprint.md`](../../templates/outputs/portfolio-sprint.md).
- [x] Write-back carve-out documented in `AGENTS.md` §7.
- [x] Reuses (does not modify) per-project Sprint Planning.
