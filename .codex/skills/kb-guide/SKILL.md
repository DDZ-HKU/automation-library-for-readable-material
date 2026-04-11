---
name: kb-guide
description: Use when the user needs a reading path, next-step guidance, or a minimal page sequence through the knowledge base
---

# KB Guide

## Overview

Use this skill to route a human through the knowledge base with the fewest pages that still preserve understanding.

## When to Use

- The user asks where to start
- The user asks what to read next
- The user wants a topic path rather than a long answer

Use `kb-ask` for direct answers and `kb-teach` for deep explanation.

## Required Flow

1. Read `wiki/INDEX.md`
2. Use `kb-locate`
3. Use `scripts/kb related <page-path>` on the likely starting page when you need nearby pages fast
4. Pick a 1 to 3 page reading path
5. Explain why each page is in the path
6. State the next hop after the path

## Output Contract

Use `agent/playbooks/reading-path-template.md`.

Always include:

- first page
- why it comes first
- what to read after it
- what is still missing from the current repo

## Do Not

- give a deep teaching answer instead of a path
- list many pages without ranking them
