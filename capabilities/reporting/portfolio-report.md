# Step 5 — Portfolio Report

> Part of [Reporting](README.md). Run on demand (e.g., monthly).
> **This is the framework's first sanctioned cross-project capability.** It is **read-only across all projects**.

## Purpose

Roll up **every project** into one portfolio view — status, phase, open-item counts, active sprint, top risk/blocker — so a portfolio/program owner can see the whole landscape at once.

## Inputs

- Every `projects/<slug>/project.md` manifest.
- Each project's `memory/*` (counts of open `REQ/ACT/Q/RSK`), current `outputs/sprints/*`, top risk.

## Procedure

1. **Enumerate projects** — read every `projects/<slug>/project.md`.
2. **Per-project row** — name/slug, domain, phase, status, sponsor, open-item counts (`REQ`/`ACT`/`Q`/`RSK`), active sprint + goal, **top risk** (`RSK-###`) and **top blocker** (`Q-###`), overall RAG.
3. **Derive per-project RAG** — green if on track, amber if a blocking question/overdue action/medium risk, red if a high risk is unmitigated or a phase goal is at risk.
4. **Portfolio roll-up** — project count, count at each RAG, aggregate open-item totals.
5. **Cross-project flags** — shared risks (e.g., the same vendor across projects), resource conflicts (same owner overloaded), common open questions.
6. **Gap check** — a project whose manifest is stale or missing memory → raise `Q-###`.

## Outputs

| Artifact | Notes |
|----------|-------|
| `reports/portfolio-<YYYY-MM-DD>.md` | **Repo root** (cross-project), not under a single project. Regenerable. |
| `memory/open-questions.md` (per project) | `Q-###` for noticed gaps, written to the relevant project. |

> **Location note:** Reports 1–4 live in `projects/<slug>/outputs/reports/` (per-project). The portfolio report lives at the **repository root** `reports/` because it spans all projects.

## Rules

- **Read-only across all projects.** No writes except optional flagging `Q-###` to a specific project.
- **Per-project isolation respected.** The report reads each project; it does not merge their IDs or memory.
- **Honest RAG.** A red project is reported red.
- **Cite slugs + IDs.** Every row names the project slug and its top risk/blocker IDs.

## Example

| Project | Domain | Phase | RAG | Open (R/A/Q/RSK) | Active sprint | Top risk | Top blocker |
|---------|--------|-------|-----|------------------|---------------|----------|-------------|
| hris | HR | build | 🟡 | 8 / 5 / 3 / 2 | S-03 | RSK-007 | Q-014 |
| inventory | Logistics | build | 🟢 | 12 / 4 / 1 / 1 | S-02 | RSK-003 | — |
| crm | Sales | discovery | 🔴 | 4 / 2 / 6 / 3 | — | RSK-001 | Q-002 |

**Roll-up:** 3 projects — 🟢×1, 🟡×1, 🔴×1. Cross-project flag: `hris` and `crm` both depend on the same SSO vendor.
