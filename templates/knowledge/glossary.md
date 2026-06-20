# Knowledge — Glossary (Template)

> Copy into `projects/<project>/knowledge/glossary.md`.
> The **glossary is the authoritative source for domain terms.** Standardize a term here once,
> then link to it everywhere else rather than redefining it.

---
doc_type: knowledge
knowledge_type: glossary
project: <project-slug>
last_reviewed: <YYYY-MM-DD>
---

# Glossary — <Project Name>

> Terms are keyed by a lowercase **slug** (e.g. `sso`, `mom`). Use the slug as the link target elsewhere.

## <slug>
- **Term:** <Full Term>
- **Definition:** <clear, one-to-two-sentence definition>
- **Synonyms / Abbreviations:** <list>
- **Related:** <other slugs or ACTOR-###/MOD-###>
- **Source:** <SRC-…>

## sso  *(example entry — remove in real use)*
- **Term:** Single Sign-On
- **Definition:** A single authentication event granting access to multiple applications without re-entering credentials.
- **Synonyms / Abbreviations:** SSO
- **Related:** identity-provider
- **Source:** <SRC-…>

## identity-provider  *(example entry)*
- **Term:** Identity Provider
- **Definition:** The system that authenticates users and issues assertions trusted by other applications.
- **Synonyms / Abbreviations:** IdP
- **Related:** sso
- **Source:** <SRC-…>

## Changelog
| Date | Editor | Change | Reason |
|------|--------|--------|--------|
| <YYYY-MM-DD> | <name> | Added `sso`, `identity-provider`. | Onboarding (<SRC-…>). |
