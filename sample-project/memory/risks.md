---
doc_type: memory
memory_type: risks
project: sample-employee-portal
last_reviewed: 2026-06-15
counter: 1
---

# Risks — Acme Employee Portal

> ⚠️ Fictional sample. One risk inferred from the kickoff timeline discussion.

## Active Risks

### RSK-001 — SSO go-live slips past July

---
id: RSK-001
title: SSO go-live slips past July
description: If Okta license confirmation (ACT-001) or Identity design (ACT-002) slips, SSO may not be live by July, delaying pilot and the August go-live.
status: identified
likelihood: medium
impact: high
mitigation: Confirm licenses by 2026-06-27 (ACT-001); set a due date for the Identity design (Q-001).
contingency: Descope pilot to internal-only users if SSO slips; push go-live.
owner: ACTOR-002
due: 2026-07-15
source: [SRC-MTG-2026-06-15]
affects: [REQ-001]
created: 2026-06-15
updated: 2026-06-15
---

The July SSO target and August go-live are tightly coupled; any slippage cascades.

## Closed / Materialized
*(none yet)*

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Created RSK-001 (counter=1). | Inferred from SRC-MTG-2026-06-15 timeline. |
