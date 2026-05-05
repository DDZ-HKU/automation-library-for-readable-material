---
title: Improving Deep Agents with Harness Engineering
updated: 2026-04-13
status: active
---

# Summary

LangChain 这组材料最有价值的，不是 benchmark 分数本身，而是展示了一条非常清晰的 harness optimization loop：用 traces 找失败模式，再把问题压缩成系统提示、middleware、上下文注入和推理预算分配这些外层改动。核心思想是，很多所谓“模型能力问题”，其实可以通过更好的 harness 被重新表述为可修复的系统问题。

## Core Points

- 他们有意把 harness 优化空间压缩到三类：
  - 系统提示
  - 工具体系
  - middleware / hooks
- traces 是整个改进闭环的核心信号：
  - 先抓运行轨迹
  - 再做并行分析
  - 再把分析结果回写成下一轮 harness 改动
- 最有效的改动包括：
  - 强制 build-verify loop
  - `PreCompletionChecklistMiddleware`
  - `LocalContextMiddleware`
  - loop detection middleware
  - 推理预算分层，即 `xhigh-high-xhigh` 的 reasoning sandwich
- 一条重要结论是：
  - harness 需要为具体模型定制

## What It Adds

- 它把 harness engineering 从抽象原则推进成“如何迭代调优”的工程循环。
- 它强调 trace 不只是 observability，而是 harness 自身的优化数据源。
- 它说明 middleware 的价值在于：
  - 不是替代模型
  - 而是在最容易出错的节点注入外部约束

## Why It Matters Here

- 当前知识库已有最小 harness 和长时运行 harness，但还没有把“怎么基于 trace 持续调优 harness”讲成独立 source 线。
- 这条线也能直接解释当前仓库为什么需要：
  - verification checkpoints
  - stop-condition checks
  - 环境信息前置注入

## Source Notes

- 来源：
  - `raw/inbox/执行框架工程让智能体从 Top 30 冲到 Top 5.md`
  - `raw/inbox/LangChain：如何通过 Harness Engineering 提升 Agent 表现_人工智能_Python编程杰哥-AtomGit开源社区.md`
- 这两份都属于 LangChain *Improving Deep Agents with Harness Engineering* 的解读链，当前作为二手汇总材料吸收。

## Related Pages

- [[agent-harness-engineering]] / [../concepts/agent-harness-engineering.md](../concepts/agent-harness-engineering.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
