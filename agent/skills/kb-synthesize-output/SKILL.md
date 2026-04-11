---
name: kb-synthesize-output
description: Use when a response may deserve persistence as an output artifact, a notes page update, or a concept page revision
---

# KB Synthesize Output

## Overview

Use this skill to decide whether a response should become a durable repository artifact.

## Decision Rules

- save to `outputs/` when the result answers a concrete question and is likely to be reused
- update `wiki/notes/` when the result captures a transferable way of thinking
- update `wiki/concepts/` when the result changes topic knowledge itself
- skip persistence when the response is short-lived and low reuse

## Required Follow-Through

When content is persisted:

- update `wiki/INDEX.md`
- append to `wiki/log.md`

Use `agent/playbooks/synthesis-template.md` to structure the decision.

## Do Not

- save everything
- write an output when a concept page update is the real need
- forget index and log updates after persistence
