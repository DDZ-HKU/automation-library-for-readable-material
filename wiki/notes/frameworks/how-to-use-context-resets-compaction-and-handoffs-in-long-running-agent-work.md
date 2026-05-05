---
title: How to Use Context Resets, Compaction, and Handoffs in Long-Running Agent Work
updated: 2026-04-13
status: active
---

# Summary

长时运行 agent 的关键问题，往往不是“还能不能继续推理”，而是“上下文变长后还能不能持续保持方向、质量和停止判断”。最稳的做法，不是默认一直堆上下文，而是把 `context reset`、`compaction` 和 `handoff artifact` 当成三种不同机制来使用：它们解决的问题不同，代价也不同。

## Confirmed Understanding

- [[harness-design-for-long-running-application-development]] / [../../sources/harness-design-for-long-running-application-development.md](../../sources/harness-design-for-long-running-application-development.md) 已确认，长任务常见两个失败模式是：
  - 随着上下文增长而失去 coherence
  - 接近上下文上限时出现 `context anxiety`
- 同一 source 也确认：
  - `context reset` 给 agent 一个 clean slate，但要求 handoff artifact 足够好
  - `compaction` 保留连续性，但不一定能消除 context anxiety
- 当前仓库的 `ops/runbook.md`、`ops/workboard.md`、`ops/handoff.md` 已经形成一套 repo-local handoff 协议：
  - 何时写 handoff
  - 什么算 natural handoff
  - handoff 前必须验证

## Tacit Interpretation

- reset、compaction、handoff 不是同义词，而是三种不同层面的控制：
  - reset 是上下文管理策略
  - compaction 是上下文压缩策略
  - handoff 是状态外置策略
- 很多长任务 agent 失败，不是因为它“不会继续做”，而是因为系统没有决定：
  - 什么时候应该换一个新上下文
  - 什么时候只该压缩旧上下文
  - 哪些状态必须外置成交接工件

## The Three Mechanisms

### 1. Context Reset

定义：

- 清空当前上下文
- 启动一个新的 agent session
- 通过 handoff artifact 把前一阶段状态交给下一阶段

适合：

- context anxiety 明显
- 长任务出现 coherence 下降
- 你希望新 agent 带着 clean slate 继续做

代价：

- orchestration 复杂度上升
- token 和 latency 增加
- handoff artifact 的质量变成关键依赖

### 2. Compaction

定义：

- 不开新 session
- 只把旧上下文压缩成更短历史

适合：

- 上下文太长，但 agent 仍保持方向
- 主要问题是 token / window 占用，而不是心理性收尾倾向

限制：

- continuity 保留了
- 但 agent 仍可能保留“快到头了要收尾”的行为倾向

### 3. Handoff Artifact

定义：

- 外部化状态、已完成项、验证结果、下一步动作、剩余风险

适合：

- 所有长任务
- 尤其是在 reset、多 session、异步恢复和自然交接点场景里

如果没有 handoff artifact：

- reset 很容易丢状态
- 续跑需要重读大量历史
- stop / continue 的边界会变模糊

## How To Think

判断该用哪种机制时，先问：

1. 当前主要问题是 window 太长，还是 agent 已经开始失去方向？
2. 当前 session 还能否可靠续跑，还是更应该换一个 clean slate？
3. 有哪些状态不能只留在 prompt 中，必须外置成工件？

一个实用规则是：

- 如果只是上下文太长，但方向没丢，优先考虑 compaction
- 如果已经出现 context anxiety 或 coherence 崩塌，优先考虑 reset
- 不管选哪种，都应该有 handoff artifact

## What a Good Handoff Must Contain

一个可用 handoff 至少要回答：

1. 当前 phase 是什么
2. 已完成了什么
3. 已验证了什么
4. 还有哪些 open risks
5. 下一次恢复时从哪里继续

这也是为什么当前仓库的 [ops/handoff.md](/Users/ddz/Documents/exp/ops/handoff.md) 结构很关键：它不是运行日记，而是恢复执行所需的最小状态包。

## How To Apply

### 在多小时 coding / app build 里

- 当模型开始出现 context anxiety，就不要只靠更强 prompt 顶住
- 应判断是否该 reset，并把 spec、contract、已完成特性和 QA 结果写成 handoff

### 在仓库自主运行里

- 让 `workboard` 提供当前目标
- 让 `runbook` 提供 continue / stop 规则
- 让 `handoff` 提供跨 session 恢复状态

### 在当前知识库仓库里

当前仓库已经把这套逻辑实现成一个轻量版本：

- `ops/workboard.md` 外置 phase 目标
- `ops/runbook.md` 定义何时继续、何时自然交接
- `ops/handoff.md` 记录交接状态

这说明 knowledge-base autonomous run 本身，也可以被视作一种 long-running harness。

## Common Mistakes

- 把 compaction 当成 reset 的完全替代
- 不写 handoff，只靠历史上下文恢复
- handoff 写成流水账，而不是最小恢复状态
- 没验证就交接，导致下一 session 从不稳定状态继续

## Source Trace

这页主要由以下资料与仓库协议提炼而来：

- [../../sources/harness-design-for-long-running-application-development.md](../../sources/harness-design-for-long-running-application-development.md)
- [../../../ops/runbook.md](../../../ops/runbook.md)
- [../../../ops/handoff.md](../../../ops/handoff.md)

## Links

- [[harness-design-for-long-running-application-development]] / [../../sources/harness-design-for-long-running-application-development.md](../../sources/harness-design-for-long-running-application-development.md)
- [[agent-harness-engineering]] / [../../concepts/agent-harness-engineering.md](../../concepts/agent-harness-engineering.md)
- [[agent-harness-minimum-architecture]] / [agent-harness-minimum-architecture.md](agent-harness-minimum-architecture.md)
