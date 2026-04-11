# Tacit Knowledge Layer Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a formal tacit-knowledge interpretation layer to this knowledge base design, then create the first human-readable tacit interpretation page based on the current RNN-to-Transformer topic line.

**Architecture:** Keep the existing `raw/`, `wiki/`, and `outputs/` structure, but explicitly define `wiki/notes/` as the home for long-lived tacit-knowledge pages. Update repository guidance so future ingest/query work knows how to distinguish explicit facts, tacit interpretations, and user-facing output artifacts.

**Tech Stack:** Markdown, repository design docs, wiki notes

---

## File Structure

- Create: `docs/superpowers/plans/2026-04-09-tacit-knowledge-layer.md`
- Create: `wiki/notes/tacit-knowledge-layer.md`
- Create: `wiki/notes/tacit-knowledge-on-rnn-to-transformer-transition.md`
- Modify: `AGENTS.md`
- Modify: `README.md`
- Modify: `wiki/INDEX.md`
- Modify: `wiki/overview.md`
- Modify: `wiki/log.md`

### Task 1: Formalize the tacit-knowledge layer in repository design

**Files:**
- Modify: `AGENTS.md`
- Modify: `README.md`
- Test: readback only

- [ ] **Step 1: Add tacit-knowledge intent to `AGENTS.md` mission and query rules**
- [ ] **Step 2: Define `wiki/notes/` as the primary home for tacit interpretation pages**
- [ ] **Step 3: Add writing guidance distinguishing explicit knowledge, tacit interpretation, and unverified inference**
- [ ] **Step 4: Add a brief repository-level explanation to `README.md` so humans can understand the new layer**
- [ ] **Step 5: Read back both files and confirm the new layer is described consistently**

### Task 2: Add a durable wiki note describing the tacit layer itself

**Files:**
- Create: `wiki/notes/tacit-knowledge-layer.md`
- Modify: `wiki/INDEX.md`
- Modify: `wiki/overview.md`
- Test: readback only

- [ ] **Step 1: Create a note that explains what tacit knowledge means in this repository**
- [ ] **Step 2: Define the standard structure of a tacit interpretation page**
- [ ] **Step 3: Update `wiki/INDEX.md` to expose the new note**
- [ ] **Step 4: Update `wiki/overview.md` to reflect the new layer in current knowledge-base design**

### Task 3: Create the first actual tacit interpretation page

**Files:**
- Create: `wiki/notes/tacit-knowledge-on-rnn-to-transformer-transition.md`
- Modify: `wiki/INDEX.md`
- Modify: `wiki/log.md`
- Test: readback only

- [ ] **Step 1: Base the page on existing wiki pages for RNNs, seq2seq-for-sets, transformers, and GPipe**
- [ ] **Step 2: Write the page in human-readable form that teaches thinking, judgment, and application**
- [ ] **Step 3: Explicitly separate confirmed understanding, tacit interpretation, and transferable judgment rules**
- [ ] **Step 4: Expose the page in `wiki/INDEX.md`**
- [ ] **Step 5: Append a log entry documenting both the design update and the first tacit page**

### Task 4: Final consistency review

**Files:**
- Modify: none unless fixes are needed
- Test: repository readback only

- [ ] **Step 1: Re-read all changed design files**
- [ ] **Step 2: Confirm the new layer does not conflict with existing raw/wiki/outputs rules**
- [ ] **Step 3: Confirm the first tacit page is linked from the index and understandable without hidden context**
