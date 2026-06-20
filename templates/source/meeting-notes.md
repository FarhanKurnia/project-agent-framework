# Meeting Notes / Transcript (Template)

> Copy into `projects/<project>/source/meetings/` as `YYYY-MM-DD-<slug>.md`.
> This is the **primary input to the Meeting Intelligence capability**.
> **Source is immutable.** Once filed, do not edit the transcript; corrections go in a follow-up note.

---
doc_type: meeting-notes
project: <project-slug>
meeting_id: <SRC-MTG-YYYY-MM-DD>     # used as provenance by extracted memory items
title: <Meeting title>
date: <YYYY-MM-DD>
time: <HH:MM–HH:MM timezone>
type: <standup | kickoff | review | planning | working | 1:1 | workshop>
location: <room / video link>
organizer: <name>
attendees: [<name>, <name>]
absent: [<name>]
recorder: <name or "transcript">
status: raw | cleaned
---

# <Meeting Title> — <YYYY-MM-DD>

## 1. Objective
<Why this meeting was held, in one or two sentences.>

## 2. Agenda
1. <Topic>
2. <Topic>

## 3. Discussion
<Narrative or verbatim transcript. This is the raw material the capability reads.
Capture what was said, by whom, in enough detail to extract requirements/decisions/actions later.>

### 3.1 <Topic>
**<Speaker>:** …

### 3.2 <Topic>
**<Speaker>:** …

## 4. Raw Decisions / Actions mentioned
<Optional scratch area. The Meeting Intelligence capability will formalize these into
`memory/decisions.md`, `memory/action-items.md`, etc. Leave informal here.>

## 5. Attachments / References
<Links to docs, slides, tickets mentioned during the meeting.>

---
<!-- Notes for the agent: -->
<!-- - Every requirement/decision/action/question extracted from this file MUST cite -->
<!--   meeting_id above as its provenance (source: [<meeting_id>]). -->
<!-- - Attendee names should be reconciled with knowledge/actors.md (ACTOR-###). -->
<!-- - If a topic is ambiguous, raise a Q-### rather than guessing. -->
