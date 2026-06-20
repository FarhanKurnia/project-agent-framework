# Capability — Reporting

> **Status:** 🟦 Specified — ready for any LLM agent to execute.
> Phase 5 capability of `project-agent-framework`. The final capability: it **synthesizes** Knowledge, Memory, and Outputs into stakeholder-facing reports. Reporting produces **no new primary data** — it reads and renders.

## Purpose

Answer the questions stakeholders actually ask: *"Where are we? What did we decide? What's risky? What's blocking us? How's the whole portfolio doing?"* — all from the single source of truth accumulated by the other capabilities, in a consistent, regenerable format.

Reporting is **read-only synthesis**. It never invents requirements, decisions, or risks; it surfaces what exists (and may raise `Q-###` to flag a gap it notices).

## Relationship to other capabilities

```
 Knowledge + Memory + Outputs (from P1–P4)
 ──────────────────────────────────────────
        │  read-only synthesis
        ▼
 ┌──────────────────────────────────────────────────────┐
 │  Reporting (P5)                                      │
 │   1. Status Report      → progress, risks, blockers  │
 │   2. Decision Log        → history + supersession    │
 │   3. Risk Report         → register + mitigation     │
 │   4. Open Questions      → aging + blockers          │
 │   5. Portfolio Report    → cross-project roll-up     │
 └──────────────────────────────────────────────────────┘
        │
        ▼
 outputs/reports/<topic>-<date>.md   (per project)
 reports/portfolio-<date>.md          (cross-project, repo root)
```

## The five reports

| Report | Question it answers | Reads | Output |
|--------|---------------------|-------|--------|
| **Status** | Where are we this period? | `memory/*`, current sprint, `knowledge/scope.md` | `outputs/reports/status-<date>.md` |
| **Decision Log** | What have we decided (and superseded)? | `memory/decisions.md` | `outputs/reports/decision-log-<date>.md` |
| **Risk** | What's risky and what's being done? | `memory/risks.md` | `outputs/reports/risk-report-<date>.md` |
| **Open Questions** | What's unresolved and aging? | `memory/open-questions.md` | `outputs/reports/open-questions-<date>.md` |
| **Portfolio** | How are all projects doing? | every `projects/<slug>/project.md` + memory | `reports/portfolio-<date>.md` (repo root) |

## Cross-cutting rules (apply to every step)

1. **Read-only synthesis.** No new primary data. A report may **raise `Q-###`** to flag a noticed gap, but never invents REQ/DEC/RSK.
2. **Cite IDs.** Every claim points to the `REQ/DEC/ACT/Q/RSK/BKL` it came from — reports are navigable, not prose-only.
3. **Honest status.** RAG ratings (red/amber/green) and risk scores reflect reality, not optimism.
4. **Date-stamped & regenerable.** Reports are named `<topic>-<YYYY-MM-DD>.md` and overwritten on re-run; history lives in git.
5. **No deletion upstream.** Reporting never modifies Source/Knowledge/Memory except to add a flagging `Q-###`.
6. **One project** for reports 1–4. **Portfolio (5) is the sanctioned cross-project exception** — read-only across all `projects/`.
7. **Follow `AGENTS.md`.** Conventions and disciplines apply.

## Step specifications

1. [`status-report.md`](status-report.md)
2. [`decision-log.md`](decision-log.md)
3. [`risk-report.md`](risk-report.md)
4. [`open-questions-report.md`](open-questions-report.md)
5. [`portfolio-report.md`](portfolio-report.md)

## How an agent runs this

> *"Generate the weekly status report for `projects/hris`."*

1. Read `AGENTS.md`, this `README.md`, and the project's full `memory/*`, current `outputs/sprints/*`, `knowledge/scope.md`.
2. Run the relevant step(s) — e.g., **Status Report** (step 1).
3. Synthesize into the template; set the date; cite IDs throughout.
4. Write `outputs/reports/<topic>-<date>.md`.
5. Report any gaps noticed as `Q-###`.

For portfolio: read every `projects/<slug>/project.md` and roll up.

## Definition of done

- [x] All five reports specified as executable procedures.
- [x] Five report templates in `templates/outputs/`.
- [x] Cross-project portfolio report defined as the sanctioned exception.
