---
name: kb-teach
description: Use when the user asks for a deeper explanation, teaching, examples, judgment, or application guidance based on a topic page or output artifact
---

# KB Teach

## Overview

Use this skill when the user wants to understand, not just receive an answer. This skill turns repository knowledge into layered explanation, judgment, and application guidance.

## When to Use

- The user says "细讲", "教我", "怎么理解", or "怎么应用"
- The user wants examples, pitfalls, or transfer rules
- The user asks about a specific `outputs/` artifact and wants it unpacked

Do not use this for plain short answers. Use `kb-ask` instead.

## Required Flow

1. Read `wiki/INDEX.md`
2. Use `kb-locate`
3. Prefer `wiki/notes/` when available
4. If the user starts from an `outputs/` artifact, read it first
5. Use `scripts/kb related <page-path>` when you need backlinks and adjacent pages
6. Backfill with relevant `concepts` and `sources`
7. Use `kb-explain-page` or its structure

## Teaching Contract

Always separate:

- explicit knowledge
- tacit interpretation
- pending inference

Default structure follows `agent/playbooks/teach-template.md`.

## Do Not

- merely summarize the page
- ignore `wiki/notes/`
- mix confirmed knowledge and interpretation without labeling them
