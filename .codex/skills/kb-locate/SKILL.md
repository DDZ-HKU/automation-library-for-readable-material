---
name: kb-locate
description: Use when another knowledge-base skill needs a stable process to find the best pages before answering, teaching, or guiding
---

# KB Locate

## Overview

This skill provides the repository's default lookup order. It keeps the agent from skipping straight to raw material or reading too many pages too early.

## Preferred Tooling

Use the repo-local search helper first:

- `scripts/kb index <pattern>` for `wiki/INDEX.md`
- `scripts/kb files <pattern>` to locate candidate pages quickly
- `scripts/kb search <pattern>` to scan `concepts`, `sources`, `notes`, and `outputs`

When the environment supports parallel tool calls, prefer running multiple narrow searches in parallel rather than one broad manual read of many files.

## Required Lookup Order

`INDEX -> concepts -> sources -> notes -> outputs -> raw`

Expanded:

1. `wiki/INDEX.md`
2. relevant `wiki/concepts/`
3. relevant `wiki/sources/`
4. relevant `wiki/notes/`
5. relevant `outputs/`
6. `raw/` only if the wiki is insufficient

## Output Contract

Return:

- primary page
- secondary pages
- reading order

## Selection Rule

- prefer concept pages for topic understanding
- prefer source pages for evidence and claims
- prefer notes for interpretation and application
- prefer outputs when the user starts from a previously produced artifact
- after `scripts/kb` narrows candidates, read only the top few pages

## Do Not

- start with `raw/`
- return a flat unranked file dump
- ignore the repo-local search helper when a quick indexed lookup would work
