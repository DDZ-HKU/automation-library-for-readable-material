# Runbook

## Startup Order

At the start of any autonomous run, read in this order:

1. `ops/charter.md`
2. `ops/workboard.md`
3. latest `ops/handoff.md`
4. `ops/runbook.md`

## Default Execution Loop

1. identify the highest-priority work item whose dependencies are satisfied
2. execute useful work toward that item
3. update relevant project files
4. check whether the work item's verification method can run
5. run verification
6. if verification fails, keep working
7. if verification passes, continue unless a natural handoff condition is reached

## Verification Rule

Verification is mandatory before handoff.

Work is not handoff-ready if:

- the artifact exists but was not checked
- a claimed phase result has not been verified

## Natural Handoff Definition

A natural handoff point is reached only when:

- the current phase goal is complete
- the phase verification methods have passed
- continuing would enter a new phase, a new risk boundary, or require a human decision

## Early Handoff Cases

Stop early and write a handoff if:

- a human decision is required
- a blocker prevents further progress
- a verification step exposes an unresolved issue that cannot be fixed inside the current phase boundary

## Handoff Types

Allowed values:

- `phase-complete`
- `decision-required`
- `blocked`

## Do Not

- stop after every subtask
- claim completion before verification
- continue into a new ambiguous phase without writing a handoff
