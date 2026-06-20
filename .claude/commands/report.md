---
description: Generate a report (read-only synthesis) — status | decisions | risk | open-questions | portfolio
argument-hint: "<type> [project-slug]  e.g. status  |  decisions hris  |  portfolio"
---

# /report — Reporting (read-only synthesis)

Generate a report of type **$ARGUMENTS**. Reporting is **read-only**: synthesize from existing data, create no new items, every claim must cite a source.

## 1. Resolve type and project
- First token = report type: `status` | `decisions` | `risk` | `open-questions` | `portfolio`.
- If empty -> show the type menu and stop.
- Second token (optional) = project slug. If empty: infer from cwd (must be inside `projects/<slug>/`). Except `portfolio` = cross-project, reads all `projects/*/`.
- `$PROJECT` = selected project.

## 2. Read capability and data sources
- Read `capabilities/reporting/<type>.md` for the chosen type + `AGENTS.md`.
- Read data: `projects/$PROJECT/memory/*` (REQ/DEC/ACT/Q/RSK/ASM), `knowledge/*`, `outputs/*`, `project.md`.
- For `portfolio`: read ALL `projects/*/memory/*` and `knowledge/*`.

## 3. Type to doc and output map
| Type | Capability doc | Output |
|------|----------------|--------|
| `status` | `status-report.md` | `projects/$PROJECT/outputs/status-report-<date>.md` |
| `decisions` | `decision-log.md` | `projects/$PROJECT/outputs/decision-log.md` |
| `risk` | `risk-report.md` | `projects/$PROJECT/outputs/risk-report.md` |
| `open-questions` | `open-questions-report.md` | `projects/$PROJECT/outputs/open-questions-report.md` |
| `portfolio` | `portfolio-report.md` | repo-root `reports/portfolio-<date>.md` |

## 4. Synthesize (read-only)
- Only summarize and structure what EXISTS in memory/knowledge.
- Do not fabricate facts/figures/status. Claims -> cite source IDs (REQ/DEC/RSK/Q + origin source).
- Flag missing data / unanswered `Q-###` as gaps; do not fill with assumptions.

## 5. Guardrails
- Follow `AGENTS.md`.
- Do not write to `memory/` (only `outputs/` / repo-root `reports/`).
- Project data is private — reports stay local, do not commit/push.

## 6. Report briefly
- Output file location + content summary (e.g. total REQ by status, recent DEC, top RSK, open Q).
