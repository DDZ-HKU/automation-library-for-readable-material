---
title: How to Separate Feedforward Guides and Feedback Sensors in Agent Harnesses
updated: 2026-04-13
status: active
---

# Summary

设计 agent harness 时，一个很常见的混乱来源是：把“事前引导 agent 不犯错”的东西，和“事后检测 agent 有没有犯错”的东西混成一类。最稳的做法是显式区分 `feedforward guides` 和 `feedback sensors`，再进一步区分它们是 `computational` 还是 `inferential`。这样才能知道哪些控制适合高频运行，哪些只适合补充语义判断。

## Confirmed Understanding

- [[harness-engineering-for-coding-agent-users]] / [../../sources/harness-engineering-for-coding-agent-users.md](../../sources/harness-engineering-for-coding-agent-users.md) 已确认，coding agent 外层 harness 至少应区分：
  - `feedforward guides`
  - `feedback sensors`
- 同一 source 也确认，这两类控制还可按执行方式分成：
  - `computational`
  - `inferential`
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md) 已确认，很多可靠性问题不该继续压给 prompt，而要进入 harness。

## Tacit Interpretation

- guide 的目标，是让 agent 更容易第一次就走在正确方向上。
- sensor 的目标，是在 agent 偏了以后尽快把偏差暴露出来。
- 如果不分这两类，就会出现两种常见误判：
  - 该前置的约束被拖到事后才发现
  - 该高频运行的检查被错误地做成昂贵的语义评估

## The Two Directions

### Feedforward Guides

这类控制在 agent 真正开始动作前就起作用。

典型对象：

- `AGENTS.md`
- rules
- coding conventions
- task-specific docs
- scoped guidance
- bootstrap scripts

它们主要回答：

- 这里该怎么做
- 有哪些边界不能碰
- 哪些默认模式是正确的

### Feedback Sensors

这类控制在 agent 产出之后或中间循环中起作用。

典型对象：

- tests
- linters
- static analysis
- review agents
- trace analysis
- browser / runtime checks

它们主要回答：

- 这次做得对不对
- 错在哪里
- 要不要继续、回退或停止

## Computational vs Inferential

### Computational

特点：

- deterministic
- 便宜
- 快
- 适合高频运行

典型对象：

- tests
- linters
- type checkers
- structural checks

### Inferential

特点：

- semantic judgment
- 更慢更贵
- 结果带概率性
- 更适合补充人类或 deterministic checks 无法覆盖的语义判断

典型对象：

- AI review
- LLM-as-judge
- semantic duplication checks
- subjective quality grading

## How To Think

设计控制时，先问两个问题：

1. 它是在事前引导，还是事后检测？
2. 它是 deterministic 运行，还是 semantic judgment？

这样就能把控制归到四个象限之一：

- feedforward + computational
- feedforward + inferential
- feedback + computational
- feedback + inferential

## How To Apply

### 在 coding agent 里

- 把 repo rules、目录地图、tool schema 放进 feedforward
- 把 tests、linters、verification scripts 放进 feedback

### 在长时运行 agent 里

- 把阶段目标、contract、handoff artifact 视作 feedforward
- 把 evaluator、checkpoint scripts、post-run review 视作 feedback

### 在知识库仓库里

- `AGENTS.md`、skills、maps、runbook 主要属于 feedforward
- verification scripts、handoff readiness checks、review loops 主要属于 feedback

## Common Mistakes

- 用事后 review 代替事前规则
- 把所有检查都做成 inferential，导致成本过高
- 把昂贵语义评估当成每一步的默认检查
- 不区分 guide 和 sensor，最后谁都不清楚控制失败发生在哪一层

## Source Trace

这页主要由以下资料提炼而来：

- [../../sources/harness-engineering-for-coding-agent-users.md](../../sources/harness-engineering-for-coding-agent-users.md)
- [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)

## Links

- [[harness-engineering-for-coding-agent-users]] / [../../sources/harness-engineering-for-coding-agent-users.md](../../sources/harness-engineering-for-coding-agent-users.md)
- [[agent-harness-engineering]] / [../../concepts/agent-harness-engineering.md](../../concepts/agent-harness-engineering.md)
