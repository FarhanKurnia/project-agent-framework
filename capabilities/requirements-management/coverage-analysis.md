# Step 5 — Coverage Analysis

> Part of [Requirements Management](README.md). Run **recurringly**, often after Categorization and Traceability.

## Purpose

Report **completeness**: which Knowledge features lack requirements (and vice-versa), and whether each scope phase is adequately covered. Coverage gaps are the leading indicator of under-specified scope.

## Inputs

- `memory/requirements.md`
- `knowledge/features.md`, `knowledge/modules.md`, `knowledge/scope.md`

## Procedure

1. **Build the coverage matrix** — features (rows) × requirements (or a feature→requirements list):
   - For each `FEAT-###`, list the `REQ-###` that deliver it.
2. **Identify forward gaps** — features with **no** requirement (or only `proposed`, not `accepted`). These are capabilities with no agreed specification.
3. **Identify reverse gaps** — requirements with **no** feature (already flagged in Traceability; here they're counted as coverage debt).
4. **Phase coverage** — for each phase in `knowledge/scope.md`, count requirements mapped to it; flag phases whose in-scope features are under-covered.
5. **Write** `outputs/reports/requirements-coverage-<date>.md` with the matrix, gap lists, and phase tallies.
6. **Raise `Q-###`** for material gaps (a Phase-1 in-scope feature with zero requirements is a blocking question, not just a stat).

## Outputs

| Artifact | Notes |
|----------|-------|
| `outputs/reports/requirements-coverage-<date>.md` | Coverage matrix + gaps + phase tallies. |
| `memory/open-questions.md` | `Q-###` for blocking coverage gaps. |

## Rules

- **Gaps are reported, not invented away.** A feature with no requirement stays a gap; do not fabricate a requirement to "fill" it.
- **Proposed ≠ covered.** Only `accepted` requirements count as coverage; `proposed` requirements are noted as partial.
- **Phase integrity.** A phase claiming a feature is in-scope but having no requirement is a planning risk — surface it loudly.
- **Report is regenerable** and should show gaps shrinking over time.

## Example

Coverage snapshot for the sample:

| Feature | Module | Requirements | Coverage |
|---------|--------|--------------|----------|
| FEAT-001 SSO Login | MOD-002 | REQ-001 (accepted) | ✅ covered |
| FEAT-002 Payslip Viewer | MOD-001 | *(none)* | ⚠️ gap — raise `Q-###` |
| FEAT-003 Leave Request | MOD-001 | *(none)* | ⚠️ gap — raise `Q-###` |

**Phase-1 coverage:** 1 of 3 in-scope features covered → Phase 1 is under-specified; two `Q-###` raised. This is exactly the kind of signal Coverage Analysis exists to produce.
