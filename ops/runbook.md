# Runbook

## Startup Order

At the start of any autonomous run, read in this order:

1. `ops/charter.md`
2. `ops/workboard.md`
3. latest `ops/handoff.md`
4. `ops/runbook.md`
5. run `scripts/ops-phase-status <project-root>`

## Default Execution Loop

1. identify the highest-priority work item whose dependencies are satisfied
2. execute useful work toward that item
3. update relevant project files
4. check whether the work item's verification method can run
5. run verification
6. if verification fails, keep working
7. run `scripts/ops-gate <project-root> batch`
8. if verification passes, continue unless a natural handoff condition is reached

## Required Script Checkpoints

The following checkpoints are mandatory when the scripts exist:

- run start:
  - `scripts/ops-phase-status <project-root>`
- after a meaningful execution batch:
  - `scripts/ops-gate <project-root> batch`
- before any claimed stop:
  - `scripts/ops-gate <project-root> stop`

Compatibility note:

- `scripts/ops-check-handoff-readiness`
- `scripts/ops-verify-continuation`

remain as thin wrappers around `scripts/ops-gate` for backwards compatibility.

If these scripts disagree with the model's instinct to stop, the scripts win.

## Verification Layers

Keep these two layers distinct:

- task-level verification:
  - the verification method attached to each work item in `ops/workboard.md`
  - answers "did this specific work item actually pass?"
- run-level gate:
  - `scripts/ops-gate <project-root> batch|stop`
  - answers "given current workboard state and handoff state, should the run continue or can it stop?"

Do not replace task-level verification with the run-level gate.
Do not use the run-level gate as evidence that a specific work item was checked.

## Anti-Stall Rules

- a progress report is not a stop condition
- finishing one subtask does not justify pausing if the phase is still active
- if no blocker exists, move directly to the next executable work item
- if an interim update is emitted, the next action in the same session should be execution, not another status report
- only stop for:
  - `phase-complete`
  - `decision-required`
  - `blocked`

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
- replace execution with progress narration when executable work still exists
- skip required continuation scripts when they exist in the project
