---
title: Agent Harness Minimum Architecture
updated: 2026-04-10
status: active
---

# Summary

一个最小可用的 agent harness，不应从“多代理协作”开始，而应从“可控闭环”开始。最小骨架必须把 LLM 限定在局部决策位置上，并由 harness 接管状态、工具执行、审批、轨迹与评估。

## Confirmed Understanding

- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md) 已确认，LLM 适合承担局部决策、比较、压缩与路由，而 harness 必须承担状态、权限、环境、trace 和 eval。
- OpenAI 的 agent 指南确认，单代理 + 工具 + 指令是更稳的起点，复杂度应逐步增加，而不是默认多代理。
- Anthropic 的 eval harness 说明确认，隔离 trial、记录轨迹、运行 grader 和聚合结果，是 agent 工程里不可缺的机械层。

## Tacit Interpretation

- “最小架构”真正要最小化的不是文件数，而是失控面。
- 如果系统里没有明确的状态边界、工具 schema 和 stop condition，那么不管 prompt 多精细，本质上都还不是一个稳定的 agent harness。
- 多数 agent 失败不是因为模型不会推理，而是因为系统没有清楚区分：
  - 模型该决定什么
  - harness 该强制什么
- 所以 harness 的最小设计目标不是“功能够多”，而是“每一步都可观测、可停止、可评分”。

## Minimum Components

最小闭环应至少包含：

1. task input layer
2. agent loop
3. tool runtime
4. state store
5. approval gate
6. trace logger
7. evaluator

## How To Think

判断一个 agent harness 是否真的成立，可以用这五个问题：

1. 当前 step 是否只能产出一种受控动作
2. 重要状态是否外置，而不是只存在 prompt 中
3. 工具是否有明确 schema 和副作用边界
4. 系统是否能在成功、失败、审批、缺信息时干净退出
5. 是否能通过 trace 和 eval 解释结果为什么变好或变差

如果这五个问题里有两个以上答不上来，系统大概率还停留在 prompt 编排，而不是 harness 工程。

## How To Apply

### 1. 从单代理最小闭环开始

- 一个模型
- 少量工具
- 明确停止条件
- 全量 trace

### 2. 先做外部状态

- working memory
- tool state
- result state

### 3. 先做工具 schema

- tool name
- arguments
- structured result
- permission level

### 4. 先做 eval，再扩复杂度

- success 样本
- failure 样本
- high-risk 样本
- wrong-tool 样本

### 5. 只在职责裂开时再拆多代理

- tool overload
- prompt overload
- 角色明显分裂

## To Be Verified

- 当前蓝图仍偏“最小单代理闭环”，尚未覆盖长期记忆、并发调度和事务性回滚。
- 对不同业务场景，approval gate 的粒度和 evaluator 维度还需要进一步细化。

## Links

- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [how-to-distinguish-architecture-optimization-and-systems-problems.md](how-to-distinguish-architecture-optimization-and-systems-problems.md)
