---
title: How to Think About Evaluation and Serving in Tool Agent Systems
updated: 2026-04-13
status: active
---

# Summary

在 tool agent 系统里，`evaluation` 和 `serving` 不是最后才补的配套层，而是系统能力本身的一部分。一个系统如果只会 `tool use`、`tool making` 或 `tool library`，却没有稳定的评估与运行分工，它更像 demo，而不是可持续运行的 agent system。

## Confirmed Understanding

- [[tool-paper-comparison-matrix]] / [tool-paper-comparison-matrix.md](tool-paper-comparison-matrix.md) 已确认，比较 tool 论文时，`evaluation` 与 `serving` 应被视为独立维度，而不是附属实现。
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md) 已确认，eval harness、trace、审批、环境和退出条件都属于系统主问题。
- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md) 已确认，ToolLLM 中 `ToolEval` 不是边角料，而是能力定义的一部分；LATM 中 maker/user 分层与 `functional cache` 也说明 serving 是核心约束，不只是部署细节。

## Tacit Interpretation

- 很多系统失败，并不是因为模型不会调用工具，而是因为系统不知道怎样判断“这次调用链算不算成功”。
- 另一些系统即使一次能跑通，也会在多次请求、长期运行、成本控制或权限边界上崩掉，这属于 serving 问题，而不是 prompt 问题。
- 因此，`evaluation` 解决的是“系统如何知道自己做对了”；`serving` 解决的是“系统如何在真实运行中稳定、可控、可复用地继续做下去”。

## Explicit Knowledge vs Interpretation

### 已确认的显性知识

- ToolLLM 把 `ToolEval` 放进主系统，说明 tool-use 不是只看调用过程，还要看结果评估。
- Agent/harness 实践明确要求：
  - trace
  - evals
  - 审批
  - 环境隔离
  - 明确退出条件
- LATM 通过 maker/user 分工与 `functional cache` 说明，多次请求场景里的成本与复用结构是系统设计的一部分。

### 默会知识解读

- 如果一个论文或系统没有认真处理 evaluation，它通常还没真正进入“可靠系统”阶段。
- 如果一个系统没有认真处理 serving，它通常只能在单次演示里表现好，而不能成为长期运行资产。
- 所以读 tool 论文或设计 agent 系统时，不应只问：
  - 会不会用工具
  - 会不会造工具
  还要问：
  - 做对了怎么判
  - 多次运行怎么稳

## Two Distinct Questions

### Evaluation 在回答什么

- 正确结果如何定义
- 多条可行路径中怎样判断一条链路足够好
- 哪些错误必须被判错，哪些差异只是路径不同
- 系统改动后能力是变好还是变差

### Serving 在回答什么

- 工具创建和工具使用如何分工
- 高成本模型和低成本模型如何搭配
- 哪些结果应该缓存，哪些不该缓存
- 长时运行时，状态、权限、审批和 handoff 如何设计

## How To Think

遇到一个 tool agent 系统时，至少问这 4 个问题：

1. 它如何判定一次任务完成？
2. 它如何记录过程，以便复查或自动评分？
3. 它如何在多次请求中控制成本、复用工具和维持边界？
4. 如果系统规模变大，evaluation 和 serving 是会强化能力，还是会先变成瓶颈？

## How To Apply

### 读论文时

- 不要只记录它的主要算法或流程。
- 额外标出：
  - 它怎么评估
  - 它怎么运行
  - 它的 serving 假设是什么

### 设计系统时

- 如果还没有明确 evaluator，就不要急着扩大工具数。
- 如果还没有明确 serving 分工，就不要急着宣称系统可长期运行。
- 如果 tool creation 已经出现，就尽快问：
  - 谁负责造
  - 谁负责用
  - 结果怎样复用

### 整理知识库时

- 看到强调 `ToolEval`、trace、grader、审批、cost-performance tradeoff、functional cache、maker/user split 的材料，不要把它们只记在“实现细节”里。
- 更合理的做法是把它们视为系统层判断，优先沉淀到 `wiki/notes/frameworks/`。

## Common Misunderstandings

- “evaluation 只是 benchmark 部分”
- “serving 只是部署工程，不影响核心能力”
- “只要模型够强，评估和运行问题会自然消失”

这些理解都容易低估 agent 系统的真实瓶颈。

## What Is Still Missing

- 当前知识库还没有专门比较不同 evaluator 设计的优劣。
- 当前知识库还没有专门整理 maker/user split 在真实项目中的实现模式。
- 关于长期运行中的状态恢复、事务边界和并发控制，仍缺更直接的材料支撑。

## Source Trace

这页主要由以下已有产物和页面提炼而来：

- [../../../outputs/tool-paper-structure-matrix-2026-04-13.md](../../../outputs/tool-paper-structure-matrix-2026-04-13.md)
- [tool-paper-comparison-matrix.md](tool-paper-comparison-matrix.md)
- [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)

## Links

- [[tool-paper-comparison-matrix]] / [tool-paper-comparison-matrix.md](tool-paper-comparison-matrix.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md)
