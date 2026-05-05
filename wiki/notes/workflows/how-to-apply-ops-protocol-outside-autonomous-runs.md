---
title: How to Apply Ops Protocol Outside Autonomous Runs
updated: 2026-04-14
status: active
---

# Summary

当前仓库里的 `ops/` 协议最初是为 `kb-autonomous-run` 这类长时自主运行设计的，但其中不少规则并不只适用于“多小时连续运行”场景。更准确的理解是：`ops/` 有一部分是 autonomous-run 专用协议，另一部分其实已经是当前仓库的一般性质量边界。这个 guide 的作用，是把两者拆开，说明哪些规则应该只在自主运行时使用，哪些规则已经值得外溢到普通 ingest / synthesis / refactor 工作中。

## Confirmed Understanding

- [ops/runbook.md](/Users/ddz/Documents/exp/ops/runbook.md) 已确认，当前 autonomous run 的核心规则包括：
  - startup order
  - default execution loop
  - required script checkpoints
  - stop condition
  - natural handoff definition
- [agent/skills/kb-autonomous-run/SKILL.md](/Users/ddz/Documents/exp/agent/skills/kb-autonomous-run/SKILL.md) 已确认，这套协议最初服务于“持续运行直到自然交接点”的工作模式。
- [how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md) 已确认，handoff artifact、stop condition 和 verification 本身是长时运行 harness 的一般机制。
- [implicit-conventions-audit-2026-04-14.md](/Users/ddz/Documents/exp/outputs/implicit-conventions-audit-2026-04-14.md) 已指出，当前边界最不清楚的地方之一就是：
  - `ops` 协议是否只限 autonomous run
  - 哪些部分已经属于全仓默认规范

## Two Layers of Ops Rules

### 1. Autonomous-Run-Specific Rules

这些规则只应在“持续执行一个 phase，直到自然交接点”的场景里启用。

典型包括：

- startup order：
  - `charter -> workboard -> handoff -> runbook`
- `scripts/ops-phase-status`
- `scripts/ops-check-handoff-readiness`
- `scripts/ops-verify-continuation`
- `phase-complete / decision-required / blocked` 这组三态 stop condition

这些规则的特点是：

- 依赖当前 phase
- 依赖当前 workboard
- 依赖 handoff artifact

所以它们不应机械套用到每一个小 query 或单页更新任务。

### 2. General Quality Rules

这些规则虽然写在 `ops/` 协议里，但实际上已经是全仓可迁移的质量边界。

典型包括：

- 不要把进度汇报当成完成
- 声称完成前要有验证
- 如果继续会跨入新风险边界，应先显式交接
- 不要在模糊边界上“顺手多做一点”而不声明

这些规则即使不在 autonomous run 里，也值得保留。

## When to Use the Full Ops Protocol

只有在下面情况，才应使用完整 `ops` 协议：

- 当前工作明确属于一个 phase
- 已有 workboard / handoff / verification method
- 目标是持续执行到自然交接点
- 允许 agent 在同一轮里跨多个子任务连续推进

典型场景：

- `kb-autonomous-run`
- 某个明确阶段的 branch synthesis
- 多轮连续 ingest / refactor / verification

## When to Apply Only the Principles

如果工作是下面这些类型，就不必机械跑完整 `ops` 协议，但仍应吸收其中的原则：

- 单次知识问答
- 单页 explanation
- 一次小型 ingest
- 一个小型 guide / output 更新

此时应继承的，是这些最小原则：

1. 不把“看起来差不多”当成完成
2. 在可验证时先验证再收尾
3. 不跨模糊边界继续扩做
4. 如果停下后下次恢复会丢状态，就写最小 handoff

## Minimal Handoff Outside Autonomous Runs

即使不在 full ops protocol 下，有时也值得写一个轻量 handoff。

适合写轻量 handoff 的情况包括：

- 工作做到一半被打断
- 已经形成了明确下一步，但不准备本轮继续
- 继续做会进入新主题线、新 phase 或新风险边界
- 当前修改已经跨多个文件或多个判断层

轻量 handoff 不必进入 `ops/handoff.md`，但至少应记录：

- 当前做到哪里
- 哪些已验证
- 下一步是什么
- 有哪些 open risks

## How To Think

判断是否该启用 full ops protocol，先问：

1. 我现在是在执行一个 phase，还是只是在处理一个局部任务？
2. 这项工作是否有明确的 done definition 和 verification method？
3. 我停下后，下一次恢复是否需要专门 handoff artifact？

如果答案偏向：

- phase / 连续执行 / 需要交接 -> 用 full ops protocol
- 局部任务 / 单次交付 / 低风险 -> 只用 general quality rules

## How To Apply in This Repo

### 对 query 工作

通常不需要 full ops protocol。

但仍应保留：

- 可验证时先验证
- 不把进度汇报当成完成
- 跨边界扩做前先声明

### 对 ingest 工作

如果只是单篇 source 摘要更新，通常不需要 full ops protocol。

如果是在做一整条主题线的批量 ingest，就更接近 autonomous run，可以考虑：

- 明确 work items
- 明确 verification
- 明确 handoff

### 对 synthesis / refactor 工作

这类工作最容易介于两者之间。

一个实用规则是：

- 如果只是单个 output 或单个 note 的更新，用原则即可
- 如果已经在连续推进一个 branch、一个 milestone 或一个长期清理任务，就该上升到 full ops protocol

## Common Mistakes

- 把 full ops protocol 生硬套到每个小任务
- 因为任务不大，就完全忽略 verification 和边界控制
- 不写 handoff，导致中断后只能靠回忆恢复
- 在小任务里偷偷跨进新主题线，却没有显式声明

## Rule of Thumb

可以把当前仓库的 `ops` 外溢规则压成一句话：

**小任务不必套完整协议，但大任务以外也应继承它的质量边界。**

## Source Trace

这页主要由以下材料收束而来：

- [ops/runbook.md](/Users/ddz/Documents/exp/ops/runbook.md)
- [agent/skills/kb-autonomous-run/SKILL.md](/Users/ddz/Documents/exp/agent/skills/kb-autonomous-run/SKILL.md)
- [how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md)
- [implicit-conventions-audit-2026-04-14.md](/Users/ddz/Documents/exp/outputs/implicit-conventions-audit-2026-04-14.md)

## Links

- [ops/runbook.md](/Users/ddz/Documents/exp/ops/runbook.md)
- [agent/skills/kb-autonomous-run/SKILL.md](/Users/ddz/Documents/exp/agent/skills/kb-autonomous-run/SKILL.md)
- [how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md)
- [implicit-conventions-audit-2026-04-14.md](/Users/ddz/Documents/exp/outputs/implicit-conventions-audit-2026-04-14.md)
