---
name: kb-ask
description: Use when the user asks a direct knowledge question and expects a concise answer grounded in this repository's wiki and outputs
---

# KB Ask

## Overview

Use this skill for direct knowledge questions. Answer from the repository's maintained knowledge first, not by recomputing from raw material.

## When to Use

- The user asks what something is
- The user asks for a comparison, summary, or judgment
- The user expects a concise answer rather than a teaching session

Do not use this for long-form teaching requests. Use `kb-teach` instead.

## Required Flow

1. Read `wiki/INDEX.md`
2. Use `kb-locate` to find the best pages
3. Read the smallest set of relevant pages from `wiki/` and `outputs/`
4. Only read `raw/` if the wiki is clearly insufficient
5. Answer with explicit source boundaries

## Answer Contract

Always distinguish:

- confirmed wiki content
- new information added during this turn
- unverified inference

Default answer order:

1. conclusion
2. key supporting pages
3. remaining gap or uncertainty

## Persistence Rule

If the answer is likely to be reused, hand off to `kb-synthesize-output`.

## Do Not

- do a full raw-material synthesis first
- skip `wiki/INDEX.md`
- turn a short answer into a teaching essay
