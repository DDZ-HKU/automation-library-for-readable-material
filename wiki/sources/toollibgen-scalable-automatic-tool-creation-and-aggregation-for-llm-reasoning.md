---
title: ToolLibGen: Scalable Automatic Tool Creation and Aggregation for LLM Reasoning
source_path: raw/sources/2510.07768v1/2510.07768v1.md
source_type: paper
author: Murong Yue; Zhiwei Liu; Liangwei Yang; Jianguo Zhang; Zuxin Liu; Haolin Chen; Ziyu Yao; Silvio Savarese; Caiming Xiong; Shelby Heinecke; Huan Wang
published: 2025
processed: 2026-04-11
topics:
  - tool-library-generation
  - tool-use
  - llm-agents
  - retrieval
entities:
  - Murong Yue
  - Zhiwei Liu
  - ToolLibGen
status: active
---

# Summary

这篇论文提出 ToolLibGen。它的核心推进不再是“让 LLM 会用工具”或“让 LLM 会造工具”，而是解决工具自动生成之后的规模化组织问题：如何把大量离散、题目特定的工具重构成可检索、可聚合、可复用的结构化工具库。

## Core Claims

- 自动化 tool making 的下一阶段瓶颈，不再是“怎么造出工具”，而是“怎么组织大量已造出的工具”。
- 当 question-specific tools 增长时，碎片化工具集合会带来检索空间膨胀和函数语义歧义。
- 因此需要把离散工具 refactor 成 structured tool library，而不是继续保留无组织的函数堆。
- Tool clustering + tool aggregation 是解决工具规模化复用的关键步骤。
- 多 agent 迭代重构比单次重构更可靠，因为要同时抽象共性、保留原始功能完整性。

## Key Facts

- ToolLibGen 的流程包含：
  - question-specific tool creation
  - tool clustering
  - tool aggregation
  - tool-augmented LLM reasoning
- 系统通过 hierarchical clustering 先把功能相关工具分组。
- 然后用 code agent + reviewing agent 的闭环，把分散功能重构成较少但更通用的 aggregated tools。
- 论文强调目标不是简单去重，而是通过更高层抽象，把工具组织成 Python library 结构。
- 实验表明相较 fragmented toolset，结构化工具库显著改善检索准确率和整体推理表现。

## Tensions / Contradictions

- 这篇工作的主问题已经不是单次任务求解，而是知识资产管理：tool making 一旦成功，新的问题变成 tool governance。
- 它与 ToolLLM / LATM 的关系类似于：前两篇解决“能力生成”，这篇解决“能力资产如何规模化组织”。
- 因此它更接近 library architecture / retrieval scaling 论文，而不是单纯推理或工具生成论文。

## Links Into Wiki

- [[tool-use-in-llms]] / [../concepts/tool-use-in-llms.md](../concepts/tool-use-in-llms.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
