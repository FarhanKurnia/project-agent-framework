---
doc_type: knowledge
knowledge_type: project-overview
project: sample-employee-portal
last_reviewed: 2026-06-15
owner: Alice Chen
---

# Project Overview — Acme Employee Portal

> ⚠️ Fictional sample. No real data.

## Summary
The Acme Employee Portal is an internal web application where employees self-service HR tasks — viewing payslips, submitting leave requests, and managing profile data. It authenticates via corporate SSO backed by Okta.

## Goals
- One centralized self-service portal for employee HR tasks.
- Corporate SSO authentication — no separate portal password.
- Phase-1 go-live with payslips, leave, and profile by August 2026.

## Non-Goals
- Manager approval workflows (deferred).
- Native mobile applications (web-first for now).

## Context
Employees currently request payslips and submit leave by emailing HR, creating manual overhead. The portal removes that friction. Acme already standardizes on Okta for identity.

## Key Facts
| Attribute | Value |
|-----------|-------|
| Domain | HR / Internal Tools |
| Phase | discovery |
| Primary sponsor | Alice Chen (ACTOR-001) |
| Tech lead | Ben Park (ACTOR-002) |
| Start date | 2026-06-15 |
| Target go-live | 2026-08-01 |

## Related Knowledge
- Actors → [`actors.md`](actors.md)
- Modules → [`modules.md`](modules.md)
- Features → [`features.md`](features.md)
- Scope → [`scope.md`](scope.md)
- Glossary → [`glossary.md`](glossary.md)

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Created. | Onboarding (SRC-MTG-2026-06-15). |
