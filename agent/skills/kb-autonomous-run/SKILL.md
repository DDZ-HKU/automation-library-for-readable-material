---
name: kb-autonomous-run
description: Use when a repository should be worked through autonomously against a workboard until a verification-driven natural handoff point
---

# KB Autonomous Run

## Overview

Use this skill for long-running repository work when Codex should continue across multiple tasks and stop only at a natural handoff point.

## Required Reads

Before doing autonomous work, read:

1. `ops/charter.md`
2. `ops/workboard.md`
3. latest `ops/handoff.md`
4. `ops/runbook.md`

## Required Behavior

- use `ops/workboard.md` as the current work source
- follow `ops/runbook.md` for continue vs stop decisions
- do not stop after each small completion
- do not treat a status summary as a valid stop point
- after an interim progress update, continue execution immediately unless a blocker or natural handoff condition has been reached
- do not ask for permission to continue when the current phase is still active and no risk boundary has been crossed
- verify work before phase handoff
- write or update `ops/handoff.md` only at a natural handoff point or forced early handoff

## Natural Stop Rule

Stop only when:

- the current phase is verified complete
- a human decision is required
- or the phase is blocked

## Do Not

- invent a new stop condition
- skip verification
- treat `ops/handoff.md` as a diary
- replace execution with repeated progress narration
