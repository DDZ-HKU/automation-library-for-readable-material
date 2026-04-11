# Autonomous Handoff Ops Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a repo-local autonomous-run layer that lets Codex keep working against a workboard until a verification-driven natural handoff point.

**Architecture:** Create an `ops/` directory for long-lived operating documents and add a project skill that forces autonomous runs through those files. Keep work definition, execution protocol, and handoff state separated so the model can continue safely without mixing roles.

**Tech Stack:** Markdown, repo-local project skills, existing wiki/index/log conventions

---

### Task 1: Create Ops Control Documents

**Files:**
- Create: `ops/charter.md`
- Create: `ops/workboard.md`
- Create: `ops/runbook.md`
- Create: `ops/handoff.md`

- [ ] **Step 1: Write the failing structure check**

Run:

```bash
test -f ops/charter.md && test -f ops/runbook.md
```

Expected: command exits non-zero before creation

- [ ] **Step 2: Create the four ops files**

The files must separate:

- long-term rules
- current work
- runtime protocol
- latest handoff

- [ ] **Step 3: Run the structure check again**

Run:

```bash
find ops -maxdepth 1 -type f | sort
```

Expected: exactly four files listed

### Task 2: Encode Verification-Driven Natural Handoff Rules

**Files:**
- Modify: `ops/charter.md`
- Modify: `ops/workboard.md`
- Modify: `ops/runbook.md`
- Modify: `ops/handoff.md`

- [ ] **Step 1: Write the failing content check**

Run:

```bash
rg -n "自然停止点|验证|phase-complete|decision-required|blocked|当前阶段|完成定义|验证方式" ops/*.md
```

Expected: missing matches before content is fully written

- [ ] **Step 2: Write `ops/charter.md`**

Must define:

- repository mission
- what counts as valuable work
- what requires human judgment
- quality and safety boundaries

- [ ] **Step 3: Write `ops/workboard.md`**

Must define:

- current stage
- work items
- priority
- dependency
- done definition
- verification method

- [ ] **Step 4: Write `ops/runbook.md`**

Must define:

- startup read order
- continuous execution loop
- when to verify
- when to continue
- when to hand off
- natural handoff definition

- [ ] **Step 5: Write `ops/handoff.md`**

Must define fields for:

- handoff type
- current phase
- completed work
- completed verification
- risks
- restart point

- [ ] **Step 6: Run the content check**

Run:

```bash
rg -n "自然停止点|验证|phase-complete|decision-required|blocked|当前阶段|完成定义|验证方式" ops/*.md
```

Expected: all required concepts present

### Task 3: Add Autonomous Run Skill

**Files:**
- Create: `agent/skills/kb-autonomous-run/SKILL.md`
- Create: `.codex/skills/kb-autonomous-run/SKILL.md`

- [ ] **Step 1: Write the failing skill check**

Run:

```bash
test -f agent/skills/kb-autonomous-run/SKILL.md && test -f .codex/skills/kb-autonomous-run/SKILL.md
```

Expected: command exits non-zero before creation

- [ ] **Step 2: Write the source skill**

Must require:

- reading `ops/charter.md`
- reading `ops/workboard.md`
- reading latest `ops/handoff.md`
- following `ops/runbook.md`
- only stopping at natural handoff points

- [ ] **Step 3: Install the project-local copy**

Mirror the same skill into `.codex/skills/`

- [ ] **Step 4: Run the skill check**

Run:

```bash
rg -n "^name: kb-autonomous-run|ops/charter.md|ops/workboard.md|ops/runbook.md|ops/handoff.md|自然停止点" agent/skills/kb-autonomous-run/SKILL.md .codex/skills/kb-autonomous-run/SKILL.md
```

Expected: all required lines matched

### Task 4: Integrate into Knowledge Base Index and Log

**Files:**
- Modify: `wiki/INDEX.md`
- Modify: `wiki/log.md`

- [ ] **Step 1: Write the failing integration check**

Run:

```bash
rg -n "kb-autonomous-run|ops/charter.md|autonomous-handoff" wiki/INDEX.md wiki/log.md
```

Expected: no matches before integration

- [ ] **Step 2: Update `wiki/INDEX.md`**

Add references to:

- the autonomous-run skill
- the `ops/` control layer

- [ ] **Step 3: Append `wiki/log.md`**

Record:

- ops layer creation
- autonomous skill installation
- handoff architecture purpose

- [ ] **Step 4: Run full verification**

Run:

```bash
find ops -maxdepth 1 -type f | sort
```

Expected: four ops files listed

Run:

```bash
find .codex/skills -maxdepth 2 -name SKILL.md | sort | rg 'kb-autonomous-run'
```

Expected: project-local autonomous skill listed

## Self-Review

- Spec coverage:
  - `ops/` structure covered in Tasks 1 and 2
  - skill layer covered in Task 3
  - repo discoverability covered in Task 4
- Placeholder scan:
  - no `TBD`, `TODO`, or unfinished markers
- Consistency:
  - same `ops/` file names used throughout

## Execution Handoff

Plan complete and saved to `docs/superpowers/plans/2026-04-11-autonomous-handoff-ops.md`.

Defaulting to inline execution because the user explicitly asked to start.
