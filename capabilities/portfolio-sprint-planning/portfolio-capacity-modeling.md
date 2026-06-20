# Step 1 — Portfolio Capacity Modeling

> Part of [Portfolio Sprint Planning](README.md). Run first, at sprint start. Extends [`../sprint-planning/capacity-modeling.md`](../sprint-planning/capacity-modeling.md) to a pool across multiple projects.

## Purpose

Compute the **pooled** capacity budget for the sprint window across all in-scope projects' contributors.

## Inputs

- In-scope project slugs (from `portfolio/manifest.md` or the user).
- The build-team roster: `portfolio/profiles/team.md` (`PERSON-###` with `availability` + `current_load`). Falls back to each project's `knowledge/actors.md` / `memory/assumptions.md` only if no roster exists.
- Sprint window; holidays/absences.
- Prior `portfolio/sprints/*` velocity (if any).

## Procedure

1. **Enumerate the contributor pool** from `portfolio/profiles/team.md` — the `PERSON-###` available to work across in-scope projects (filter `status: active`). Enforce a **per-person ceiling**: each PERSON's capacity = `availability` − `current_load` (see [load-reconciliation](../profile-management/load-reconciliation.md)). Team total = sum of per-person ceilings.
2. **Compute available time** per contributor (working days − holidays − absences × availability %). Sum to a portfolio total.
3. **Apply a focus factor** (~20–30%); state it.
4. **Convert to a budget** — points if portfolio velocity exists, else ideal-days flagged as an estimate (the first portfolio sprint has no history).
5. **Record assumptions** as `ASM-###` in each relevant project's `memory/assumptions.md` (provenance: the portfolio planning source).
6. **Write** the pooled budget into the sprint artifact's *Capacity* section.

## Rules

- **Honest capacity.** Do not inflate; subtract deductions.
- **No velocity → estimate + flag.**
- **Per-project assumptions stay per-project.** An assumption about `hris` staffing lives in `hris/memory/assumptions.md`, not in the portfolio artifact.

## Example

Window 2026-07-06 → 2026-07-19 (10 working days). Pool: FE/BE @ employee-portal (100%), QA @ employee-portal (50%), BE @ helpdesk (100%). Focus 25%. Raw = 9 + 4.5 + 9 = 22.5 days → ~17 ideal-days. Budget: **~17 ideal-days** (estimate, no velocity).
