---
title: Harness Design for Long-Running Application Development
updated: 2026-04-13
status: active
---

# Summary

Anthropic 这篇文章讨论的不是最小 agent harness，而是如何把 harness 推到“多小时、跨阶段、接近完整应用开发”的长时运行形态。它的关键贡献是把 earlier harness 中的 context reset、structured handoff 和 evaluator 思路继续推进成 planner / generator / evaluator 的三代理结构，并强调长时任务中上下文管理与外部评估者的重要性。

## Core Points

- naive 长任务 agent 常见两个失败模式：
  - context window 增长带来的 coherence 丢失
  - agent 自评过于宽松
- 对某些模型，仅靠 compaction 不够，context reset + structured handoff 才能真正缓解 context anxiety。
- 在 frontend design 与 long-running coding 两个场景里，一个共同杠杆是：
  - generator 与 evaluator 分离
- 长时应用开发 harness 采用了三代理分工：
  - `planner`
  - `generator`
  - `evaluator`
- generator 与 evaluator 会在每个 sprint 前先协商 sprint contract，把高层 spec 压成可测试的交付边界。
- communication 通过文件工件完成，使跨 session handoff 结构化。

## What It Adds

- 它把 harness 从“最小闭环”推进到“多小时构建循环”。
- 它明确说明，长时 agent 的关键难点不是单次推理，而是：
  - 上下文续接
  - 质量评估
  - 任务切块
  - session handoff
- 它也说明主观任务与可验证任务之间，可以共享某些 harness 技巧，比如外部 evaluator 和结构化 contract。

## Why It Matters Here

- 当前知识库已有最小 harness 框架，这篇资料补了“长时运行时 harness 会长成什么样”。
- 它直接支撑了当前仓库里 `ops/runbook`、`workboard`、handoff 工件这类长期运行协议的解释空间。

## Source Notes

- 来源：`raw/inbox/Harness design for long-running application development.md`
- 原文：Anthropic，2026

## Related Pages

- [[agent-harness-minimum-architecture]] / [../notes/frameworks/agent-harness-minimum-architecture.md](../notes/frameworks/agent-harness-minimum-architecture.md)
- [[agent-harness-engineering]] / [../concepts/agent-harness-engineering.md](../concepts/agent-harness-engineering.md)
