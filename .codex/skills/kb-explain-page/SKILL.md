---
name: kb-explain-page
description: Use when a knowledge-base page or output artifact needs a structured explanation that goes beyond summary
---

# KB Explain Page

## Overview

Use this skill to unpack a single page or artifact in a way that makes its role in the repository legible.

## Preferred Tooling

When the page path is known, use `scripts/kb related <page-path>` first to gather backlinks and nearby outputs before explaining the page in isolation.

## Required Structure

1. what this page is saying
2. why it matters
3. what topic line it belongs to
4. what people are likely to misunderstand
5. how to use it in research or application
6. what is still missing

## Constraints

- do not merely summarize
- add page-to-page relations
- add application guidance
- if inference appears, label it

## Common Inputs

- a `wiki/concepts/` page
- a `wiki/notes/` page
- an `outputs/` artifact
