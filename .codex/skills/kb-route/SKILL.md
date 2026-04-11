---
name: kb-route
description: Use when a knowledge-base request needs to be routed to the right skill before reading many pages or generating a long answer
---

# KB Route

## Overview

Use this skill as the front door for the repo's knowledge workflows.

## Intent Mapping

- direct question -> `kb-ask`
- teaching request -> `kb-teach`
- navigation request -> `kb-guide`
- persistence request -> `kb-synthesize-output`

Typical wording:

- "是什么", "比较", "总结", "为什么" -> `kb-ask`
- "细讲", "教我", "怎么理解", "怎么应用" -> `kb-teach`
- "拆解这个产物", "讲懂这份 memo", "详细解释这页输出" -> `kb-teach`
- "从哪开始", "先看什么", "下一步" -> `kb-guide`
- "先看哪个 output", "已有哪份产物最相关" -> `kb-guide`
- "保存", "沉淀", "写成产物" -> `kb-synthesize-output`

## Constraints

- do not answer at length
- choose the next skill and stop
- if unsure between `kb-ask` and `kb-teach`, choose `kb-teach` when the user asks for method, judgment, or examples
- if the user asks both "what is it" and "what should I read next", choose `kb-guide` first
