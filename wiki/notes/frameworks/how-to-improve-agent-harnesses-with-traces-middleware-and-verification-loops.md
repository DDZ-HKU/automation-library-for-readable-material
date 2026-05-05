---
title: How to Improve Agent Harnesses with Traces, Middleware, and Verification Loops
updated: 2026-04-13
status: active
---

# Summary

当一个 agent 已经能基本跑起来后，下一阶段的关键问题往往不是“换个更强模型”，而是“如何用 traces、middleware 和 verification loop 持续调优 harness”。这类优化的核心，不是让模型更会说，而是让系统更会发现失败模式、更会在关键节点插入约束、更会强迫 agent 面对真实反馈。

## Confirmed Understanding

- [[improving-deep-agents-with-harness-engineering]] / [../../sources/improving-deep-agents-with-harness-engineering.md](../../sources/improving-deep-agents-with-harness-engineering.md) 已确认，traces 是发现 harness 缺陷的主要反馈信号。
- 同一 source 也确认，最有效的改进集中在：
  - 自验证循环
  - 上下文注入
  - loop detection
  - 推理预算分层
- [[agent-harness-minimum-architecture]] / [agent-harness-minimum-architecture.md](agent-harness-minimum-architecture.md) 已确认，没有 trace 和 evaluator，就很难把 agent 系统调成可解释、可比较的状态。

## Tacit Interpretation

- 很多失败并不是“模型不会”，而是：
  - 环境信息没给够
  - 验证步骤没强制
  - bad loop 没被及时打断
  - 推理预算分配错了
- middleware 的价值就在这里：它不是重新定义 agent，而是在最容易出错的节点施加可重复约束。
- traces 则把“感觉 agent 经常在某处出错”变成了可分析的工程对象。

## Three Main Levers

### 1. Traces

traces 的用途不是只做 observability，而是做 harness optimization。

它至少应该帮助回答：

- agent 卡在哪一步
- 错误更常来自推理、工具、环境还是验证
- 某种失败模式是不是重复出现

### 2. Middleware

middleware 适合插在这些节点：

- 任务启动时
- 退出前
- 重复编辑某个对象过多时
- 缺环境上下文时

典型例子：

- `LocalContextMiddleware`
- `PreCompletionChecklistMiddleware`
- `LoopDetectionMiddleware`

### 3. Verification Loops

一个稳的 loop 通常是：

1. build
2. verify
3. read result
4. fix

关键在于：

- 不是让 agent 自己“觉得已经完成”
- 而是让它面对真实测试或环境反馈

## How To Think

当 agent 表现不稳定时，优先按下面顺序排查：

1. 是不是缺 trace，根本看不见失败模式？
2. 是不是缺 verification gate，导致 agent 太早宣布完成？
3. 是不是缺环境注入，导致 agent 花太多步骤找上下文？
4. 是不是缺 loop detection，导致 agent 死循环？
5. 是不是推理预算分配错了？

## How To Apply

### 先做 traces

- 没有 traces，就很难知道该改 harness 的哪一层

### 再做 verification gate

- 先强制 build-verify loop
- 再去优化更细的 prompt 或 route

### 再做 middleware

- 把最常见失败模式变成中间件插点

### 最后才调更细的模型适配

- 比如不同模型的推理预算、提示风格和 loop 节奏

## Common Mistakes

- 一上来就换模型，不先看 traces
- 让 agent 用自我感觉判断“做完了”
- 发现死循环后，只靠 prompt 提醒，不做 middleware
- 把所有问题都归因于 reasoning，而忽略环境注入和验证缺失

## Source Trace

这页主要由以下资料提炼而来：

- [../../sources/improving-deep-agents-with-harness-engineering.md](../../sources/improving-deep-agents-with-harness-engineering.md)
- [agent-harness-minimum-architecture.md](agent-harness-minimum-architecture.md)

## Links

- [[improving-deep-agents-with-harness-engineering]] / [../../sources/improving-deep-agents-with-harness-engineering.md](../../sources/improving-deep-agents-with-harness-engineering.md)
- [[agent-harness-engineering]] / [../../concepts/agent-harness-engineering.md](../../concepts/agent-harness-engineering.md)
- [[agent-harness-minimum-architecture]] / [agent-harness-minimum-architecture.md](agent-harness-minimum-architecture.md)
