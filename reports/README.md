# reports/

This directory holds **cross-project (portfolio) reports** — the output of the Reporting capability's [Portfolio Report](../capabilities/reporting/portfolio-report.md) step.

## What lives here

- `portfolio-<YYYY-MM-DD>.md` — a read-only roll-up across **all** projects under `projects/`, generated from each project's `project.md` manifest and memory.

## How this differs from per-project reports

- **Per-project reports** (status, decision-log, risk, open-questions) live inside each project at `projects/<slug>/outputs/reports/`. They are scoped to one project.
- **Portfolio reports** live **here** at the repository root, because they intentionally span every project. This is the framework's only sanctioned cross-project location.

## Rules

- **Read-only synthesis.** Portfolio reports read across projects; they do not merge IDs or memory, and they write nothing except (optionally) a flagging `Q-###` back into a specific project.
- **Regenerable.** Files are named with a date and overwritten on re-run; history is kept in git.
- **No project data committed here.** This directory contains only generated portfolio reports and this README — never raw project source/knowledge/memory.
