---
title: CREATOR: Tool Creation for Disentangling Abstract and Concrete Reasoning of Large Language Models
source_path: raw/sources/2305.14318v3/2305.14318v3.md
source_type: paper
author: Cheng Qian; Chi Han; Yi R. Fung; Yujia Qin; Zhiyuan Liu; Heng Ji
published: 2023
processed: 2026-04-11
topics:
  - tool-creation
  - llm-agents
  - tool-use
  - reasoning
entities:
  - Cheng Qian
  - Chi Han
  - Yujia Qin
  - Zhiyuan Liu
  - Heng Ji
  - CREATOR
status: active
---

# Summary

这篇论文提出 CREATOR。它的关键推进在于不把 LLM 看成单纯的 tool user，而是把 problem solving 拆成四个阶段：creation、decision、execution、rectification，并明确强调应当把抽象工具创建与具体决策执行解耦。

## Core Claims

- 现有 tool-augmented LLM 的问题不仅是工具数量有限，还包括：
  - reasoning fragility
  - scope limitation
  - error handling insufficiency
- 因此关键不只是给更多工具，而是让 LLM 能自己创造更一般、更可复用的工具。
- 创造工具与使用工具不该混成同一步，而应解耦成：
  - abstract reasoning for creation
  - concrete reasoning for decision
- code 作为工具创建媒介，能够让错误更显式暴露，并支持后续 automatic rectification。
- 这种 creation / decision disentanglement 能提高准确率和鲁棒性。

## Key Facts

- CREATOR 的四阶段是：
  - Creation
  - Decision
  - Execution
  - Rectification
- 论文在 MATH、TabMWP 和自建 Creation Challenge 上评估该框架。
- CREATOR 相比 CoT、PoT 和普通 tool-using baselines 有显著提升。
- 作者特别强调 hints 与 stage separation 会显著影响 tool creation 成功率。
- Rectification stage 可以进一步修正 tool 和 decision，提高稳定性。

## Tensions / Contradictions

- 这篇论文和 LATM 都属于 tool creation 方向，但 CREATOR 更强调“认知分工”和 reasoning disentanglement，而 LATM 更强调“serving cost 分工”和 functional cache。
- 因此它更像 tool creation 的认知/推理结构论文，而不只是 serving architecture 论文。
- 它与 ToolLLM 的关系也不是替代，而是进一步说明：在真实 tool use 之外，tool creation 本身也需要被拆阶段。

## Links Into Wiki

- [[tool-use-in-llms]] / [../concepts/tool-use-in-llms.md](../concepts/tool-use-in-llms.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
