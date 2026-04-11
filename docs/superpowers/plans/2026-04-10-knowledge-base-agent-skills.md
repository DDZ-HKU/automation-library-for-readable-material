# Knowledge Base Agent Skills Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a repo-local knowledge-base skill layer with 7 skills, shared playbooks, and lightweight maps so agents can query, teach, route, and synthesize knowledge using this wiki-first repository.

**Architecture:** Store repo-specific skills under `agent/skills/`, with one `SKILL.md` per skill. Keep common answer shapes in `agent/playbooks/` and fast navigation artifacts in `agent/maps/`. Validate behavior with structure checks and content checks rather than application tests, because the deliverable is an agent workflow/documentation system.

**Tech Stack:** Markdown, repo-local skill conventions, ripgrep-based verification

---

### Task 1: Create Agent Skill Layer Skeleton

**Files:**
- Create: `agent/skills/kb-ask/SKILL.md`
- Create: `agent/skills/kb-teach/SKILL.md`
- Create: `agent/skills/kb-guide/SKILL.md`
- Create: `agent/skills/kb-locate/SKILL.md`
- Create: `agent/skills/kb-explain-page/SKILL.md`
- Create: `agent/skills/kb-synthesize-output/SKILL.md`
- Create: `agent/skills/kb-route/SKILL.md`
- Create: `agent/playbooks/answer-template.md`
- Create: `agent/playbooks/teach-template.md`
- Create: `agent/playbooks/reading-path-template.md`
- Create: `agent/playbooks/synthesis-template.md`
- Create: `agent/maps/topic-lines.md`
- Create: `agent/maps/high-value-pages.md`
- Create: `agent/maps/outputs-index.md`

- [ ] **Step 1: Write the failing structure check**

Run:

```bash
test -f agent/skills/kb-ask/SKILL.md && test -f agent/maps/topic-lines.md
```

Expected: command exits non-zero because files do not exist yet

- [ ] **Step 2: Create the directory structure and placeholder-free files**

Create this tree:

```text
agent/
  skills/
    kb-ask/SKILL.md
    kb-teach/SKILL.md
    kb-guide/SKILL.md
    kb-locate/SKILL.md
    kb-explain-page/SKILL.md
    kb-synthesize-output/SKILL.md
    kb-route/SKILL.md
  playbooks/
    answer-template.md
    teach-template.md
    reading-path-template.md
    synthesis-template.md
  maps/
    topic-lines.md
    high-value-pages.md
    outputs-index.md
```

- [ ] **Step 3: Run the structure check again**

Run:

```bash
find agent -maxdepth 3 -type f | sort
```

Expected: all 14 files listed

### Task 2: Implement High-Frequency Entry Skills

**Files:**
- Modify: `agent/skills/kb-ask/SKILL.md`
- Modify: `agent/skills/kb-teach/SKILL.md`
- Modify: `agent/skills/kb-guide/SKILL.md`
- Create: `agent/playbooks/answer-template.md`
- Create: `agent/playbooks/teach-template.md`
- Create: `agent/playbooks/reading-path-template.md`

- [ ] **Step 1: Write the failing content check for entry skills**

Run:

```bash
rg -n "^name: kb-ask|^name: kb-teach|^name: kb-guide|wiki/INDEX.md|kb-locate" agent/skills/kb-ask/SKILL.md agent/skills/kb-teach/SKILL.md agent/skills/kb-guide/SKILL.md
```

Expected: missing matches until the files are fully authored

- [ ] **Step 2: Write `kb-ask`**

Required content:

```md
---
name: kb-ask
description: Use when the user asks a direct knowledge question and expects a concise answer grounded in this repository's wiki and outputs
---
```

Body must include:

- trigger conditions
- mandatory first read of `wiki/INDEX.md`
- mandatory use of `kb-locate`
- distinction between confirmed wiki content, new additions, and unverified inference
- optional handoff to `kb-synthesize-output`

- [ ] **Step 3: Write `kb-teach`**

Required content:

```md
---
name: kb-teach
description: Use when the user asks for a deeper explanation, teaching, examples, judgment, or application guidance based on a topic page or output artifact
---
```

Body must include:

- preference for `wiki/notes/`
- output structure aligned with `agent/playbooks/teach-template.md`
- explicit distinction between explicit knowledge, tacit interpretation, and pending inference

- [ ] **Step 4: Write `kb-guide`**

Required content:

```md
---
name: kb-guide
description: Use when the user needs a reading path, next-step guidance, or a minimal page sequence through the knowledge base
---
```

Body must include:

- route for “from where should I start” and “what should I read next”
- 1 to 3 page reading path rule
- use of `kb-locate`

- [ ] **Step 5: Write shared playbooks for answer, teaching, and reading paths**

Each file must define a fixed output skeleton the skills can reference.

- [ ] **Step 6: Run the entry skill content check**

Run:

```bash
rg -n "^name: kb-ask|^name: kb-teach|^name: kb-guide|wiki/INDEX.md|kb-locate|wiki/notes|1 to 3" agent/skills/kb-ask/SKILL.md agent/skills/kb-teach/SKILL.md agent/skills/kb-guide/SKILL.md
```

Expected: all required strings matched

### Task 3: Implement Execution Skills

**Files:**
- Modify: `agent/skills/kb-locate/SKILL.md`
- Modify: `agent/skills/kb-explain-page/SKILL.md`
- Modify: `agent/skills/kb-synthesize-output/SKILL.md`
- Modify: `agent/skills/kb-route/SKILL.md`
- Create: `agent/playbooks/synthesis-template.md`

- [ ] **Step 1: Write the failing content check for execution skills**

Run:

```bash
rg -n "wiki/INDEX.md|wiki/concepts|wiki/sources|wiki/notes|outputs|raw|kb-ask|kb-teach|kb-guide|INDEX.md|log.md" agent/skills/kb-locate/SKILL.md agent/skills/kb-explain-page/SKILL.md agent/skills/kb-synthesize-output/SKILL.md agent/skills/kb-route/SKILL.md
```

Expected: missing matches until implementation is complete

- [ ] **Step 2: Write `kb-locate`**

Body must enforce this exact order:

```text
INDEX -> concepts -> sources -> notes -> outputs -> raw
```

and return:

- primary page
- secondary pages
- reading order

- [ ] **Step 3: Write `kb-explain-page`**

Body must require:

- not merely summarizing
- page role in a topic line
- likely confusions
- application guidance

- [ ] **Step 4: Write `kb-synthesize-output`**

Body must define when to:

- save to `outputs/`
- update `wiki/notes/`
- update `wiki/concepts/`
- skip saving entirely

It must also require `wiki/INDEX.md` and `wiki/log.md` updates when content is persisted.

- [ ] **Step 5: Write `kb-route`**

Body must map:

- direct question -> `kb-ask`
- teaching request -> `kb-teach`
- navigation request -> `kb-guide`
- persistence request -> `kb-synthesize-output`

- [ ] **Step 6: Write `agent/playbooks/synthesis-template.md`**

Include fields for:

- artifact type
- target path
- summary
- why it deserves persistence
- follow-on wiki updates

- [ ] **Step 7: Run the execution skill content check**

Run:

```bash
rg -n "INDEX -> concepts -> sources -> notes -> outputs -> raw|wiki/log.md|wiki/INDEX.md|kb-ask|kb-teach|kb-guide|outputs/|wiki/notes/|wiki/concepts/" agent/skills/kb-locate/SKILL.md agent/skills/kb-synthesize-output/SKILL.md agent/skills/kb-route/SKILL.md
```

Expected: all required routing and persistence rules matched

### Task 4: Implement Fast Navigation Maps

**Files:**
- Modify: `agent/maps/topic-lines.md`
- Modify: `agent/maps/high-value-pages.md`
- Modify: `agent/maps/outputs-index.md`

- [ ] **Step 1: Write the failing map check**

Run:

```bash
rg -n "RNN/LSTM|attention|Transformer|overview|INDEX|outputs" agent/maps/topic-lines.md agent/maps/high-value-pages.md agent/maps/outputs-index.md
```

Expected: missing matches until maps are populated

- [ ] **Step 2: Populate `topic-lines.md`**

Include at least:

```md
- `RNN/LSTM -> Bahdanau attention -> Transformer -> pipeline parallelism`
```

with linked page paths

- [ ] **Step 3: Populate `high-value-pages.md`**

Include:

- repo entry pages
- core concept pages
- tacit knowledge pages
- high-value outputs

- [ ] **Step 4: Populate `outputs-index.md`**

List existing outputs with:

- path
- one-line purpose
- when to reuse them

- [ ] **Step 5: Run the map check**

Run:

```bash
rg -n "RNN/LSTM|Bahdanau|Transformer|wiki/INDEX.md|wiki/overview.md|outputs/rnn-transformer-research-decision-memo-2026-04-09.md" agent/maps/topic-lines.md agent/maps/high-value-pages.md agent/maps/outputs-index.md
```

Expected: all key lines matched

### Task 5: Repository Integration and Verification

**Files:**
- Modify: `wiki/INDEX.md`
- Modify: `wiki/log.md`
- Optionally modify: `wiki/notes/workflows/` if a stable workflow page is warranted

- [ ] **Step 1: Write the failing integration check**

Run:

```bash
rg -n "knowledge-base-agent-skills|agent/skills|agent/maps" wiki/INDEX.md wiki/log.md
```

Expected: no matches before integration update

- [ ] **Step 2: Update `wiki/INDEX.md` if these agent assets should be discoverable**

Add a concise reference to the new agent skill layer in a fitting section or create a small operations section.

- [ ] **Step 3: Append a `wiki/log.md` entry**

Record:

- creation of the skill layer
- new playbooks
- new maps

- [ ] **Step 4: Run full verification**

Run:

```bash
find agent -maxdepth 3 -type f | sort
```

Expected: all skill, playbook, and map files listed

Run:

```bash
rg -n "^name: kb-|^description: Use when" agent/skills/*/SKILL.md
```

Expected: seven skills with valid frontmatter names and “Use when” descriptions

Run:

```bash
rg -n "wiki/INDEX.md|kb-locate|kb-synthesize-output|wiki/log.md" agent/skills/*/SKILL.md
```

Expected: cross-skill workflow hooks present

## Self-Review

- Spec coverage:
  - 7-skill structure covered in Tasks 1 to 3
  - playbooks covered in Tasks 2 and 3
  - maps covered in Task 4
  - repo discoverability and logging covered in Task 5
- Placeholder scan:
  - no `TBD`, `TODO`, or “implement later” markers
- Consistency:
  - all tasks use the same skill names and same `agent/` path layout

## Execution Handoff

Plan complete and saved to `docs/superpowers/plans/2026-04-10-knowledge-base-agent-skills.md`.

Defaulting to inline execution because the user explicitly asked to start implementation now.
