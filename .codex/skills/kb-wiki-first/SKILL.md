---
name: kb-wiki-first
description: Use when working anywhere in this repository and the task touches repository knowledge, outputs, interpretation, or source ingestion decisions
---

# KB Wiki First

## Overview

This is the project entry skill for the repository. It tells Codex to treat this repo as a maintained knowledge base, not a loose file pile.

## Core Rule

For knowledge tasks, the default order is:

1. `wiki/INDEX.md`
2. relevant `wiki/` pages
3. relevant `outputs/`
4. `raw/` only if the wiki is insufficient

## Preferred Tooling

Prefer the repo-local helper before ad-hoc searching:

- `scripts/kb index <pattern>`
- `scripts/kb files <pattern>`
- `scripts/kb search <pattern>`

If multiple search angles are needed, use parallel search calls across concepts, sources, notes, and outputs.

## When to Use

- answering a knowledge question
- explaining a topic or an existing output
- deciding what to read next
- deciding whether a result should be persisted
- continuing an ingest or knowledge-organization task

## Required Routing

- direct knowledge request -> `kb-route`
- deep explanation request -> `kb-route`, which should choose `kb-teach`
- reading-path request -> `kb-route`, which should choose `kb-guide`
- persistence decision -> `kb-route`, which should choose `kb-synthesize-output`

## Repository Contract

- `raw/` is readable source material and should not be rewritten
- `wiki/` is maintained knowledge and should be preferred during query work
- `outputs/` stores reusable answers, reports, and intermediate research products
- `wiki/notes/` stores tacit knowledge, judgment frameworks, and application guidance

## Do Not

- answer from `raw/` first when `wiki/` already covers the topic
- treat `outputs/` as disposable chat transcripts
- collapse explicit knowledge and tacit interpretation into one unlabeled block
- skip the repo-local search helper when the task is clearly a knowledge lookup
