---
title: Harness Engineering for Coding Agent Users
updated: 2026-04-13
status: active
---

# Summary

Thoughtworks 这篇文章把 coding agent 场景里的 harness 明确限定为“模型之外、由用户和团队为具体代码库构建的外层控制系统”。它最重要的贡献不是再强调 prompt，而是把 harness 拆成 `feedforward guides` 与 `feedback sensors`，并进一步区分 `computational` 与 `inferential` 两类执行方式。

## Core Points

- harness 在 coding agent 语境下，不是单一 prompt，而是围绕 agent 的外层控制结构。
- 一个好的 outer harness 同时做两件事：
  - 提高 agent 第一次就做对的概率
  - 在结果到达人类前尽量自我纠错
- guides / sensors 可按执行类型分成：
  - `computational`
  - `inferential`
- harness 进一步可按调节对象分成：
  - `maintainability harness`
  - `architecture fitness harness`
  - `behaviour harness`
- harnessability 不是默认存在的，代码库本身是否强类型、模块边界是否清楚、工具链是否成熟，会直接决定 harness 能做多强。

## What It Adds

- 它把“harness”这个过宽术语缩进到 coding agent 的具体边界里。
- 它提醒我们，真正能高频运行的是 deterministic computational controls，而 inferential controls 更适合补语义判断。
- 它把 harness 从“单次交互技巧”上升为持续改进的 steering loop：重复出现的问题应被回写成更好的 guides 或 sensors。

## Why It Matters Here

- 这篇文章补强了当前知识库里对 harness 的一个缺口：不仅要讨论状态、eval 和 stop condition，还要讨论 feedforward 与 feedback 如何分布在开发生命周期里。
- 它也把“人类掌舵”从抽象口号推进成了一个明确动作：人类不断迭代 harness，而不是不断手工纠正 agent。

## Source Notes

- 来源：`raw/inbox/Harness engineering for coding agent users.md`
- 原文：Martin Fowler / Thoughtworks，2026-04-02

## Related Pages

- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
- [[agent-harness-engineering]] / [../concepts/agent-harness-engineering.md](../concepts/agent-harness-engineering.md)
