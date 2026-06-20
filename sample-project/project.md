---
doc_type: project-manifest
project: sample-employee-portal
name: Acme Employee Portal
slug: sample-employee-portal
domain: HR / Internal Tools
phase: discovery
status: active
sponsor: Alice Chen
tech_lead: Ben Park
product_owner: Alice Chen
key_contacts:
  - ACTOR-001   # Alice Chen — Product Owner
  - ACTOR-002   # Ben Park — Tech Lead
created: 2026-06-15
target_go_live: 2026-08-01
description: >
  A fictional internal self-service portal where Acme employees view payslips,
  submit leave requests, and manage profile data, authenticated via corporate SSO.
  Used purely to demonstrate project-agent-framework — contains no real data.
---

# Acme Employee Portal — Project Manifest

> ⚠️ **This is a sample project.** All names, dates, and content are fictional.
> It exists to demonstrate the framework end-to-end. Do not treat as real business data.

## Summary
The Acme Employee Portal gives employees a single self-service entry point for HR tasks: payslips, leave, and profile. It authenticates via corporate SSO. This sample shows one kickoff meeting processed through the full Meeting Intelligence pipeline.

## Goals
- Centralize employee self-service in one portal.
- Use corporate SSO (no separate portal passwords).
- Go live with a minimum viable feature set by August 2026.

## Non-Goals (Phase 1)
- Manager approvals workflow (deferred to a later phase).
- Mobile native apps (web-first for now).

## Related Knowledge
- Overview → [`knowledge/project-overview.md`](knowledge/project-overview.md)
- Actors → [`knowledge/actors.md`](knowledge/actors.md)
- Modules → [`knowledge/modules.md`](knowledge/modules.md)
- Features → [`knowledge/features.md`](knowledge/features.md)
- Scope → [`knowledge/scope.md`](knowledge/scope.md)

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| 2026-06-15 | agent | Created manifest + Knowledge + Memory skeleton. | Onboarding (SRC-MTG-2026-06-15). |
