---
title: ToolLLM: Facilitating Large Language Models to Master 16000+ Real-World APIs
source_path: raw/sources/2307.16789v2/2307.16789v2.md
source_type: paper
author: Yujia Qin; Shihao Liang; Yining Ye; Kunlun Zhu; Lan Yan; Yaxi Lu; Yankai Lin; Xin Cong; Xiangru Tang; Bill Qian; Sihan Zhao; Lauren Hong; Runchu Tian; Ruobing Xie; Jie Zhou; Mark Gerstein; Dahai Li; Zhiyuan Liu; Maosong Sun
published: 2023
processed: 2026-04-11
topics:
  - tool-use
  - toolllm
  - llm-agents
  - evaluation
entities:
  - Yujia Qin
  - Shihao Liang
  - Yining Ye
  - ToolBench
  - ToolEval
  - ToolLLaMA
status: active
---

# Summary

这篇论文提出 ToolLLM 框架，目标是让开源 LLM 获得接近闭源模型的 tool-use 能力。它的关键贡献不是单个模型结构，而是把工具使用问题拆成一个完整系统：大规模 API 数据集、自动构造流程、训练模型、API 检索器、搜索式推理策略和自动评估器。

## Core Claims

- 当前开源 LLM 的弱点之一不是语言本身，而是 tool-use domain 没有被系统纳入 instruction tuning。
- 真实工具使用不是单工具调用，而是涉及：
  - 大规模 API 选择
  - 多步规划
  - 多轮执行
  - API 返回值驱动的后续决策
- 因此要提升 tool use，不能只靠 prompt engineering，而需要同时建设：
  - dataset
  - reasoning strategy
  - retrieval
  - evaluator
- DFSDT 比单路径 ReACT 更适合这类 tool-use 决策空间，因为它允许比较多条 reasoning trace 并做回退。
- ToolEval 说明 tool-use 的评估必须考虑“多条正确路径可能并存”，不能只用单一路径匹配。

## Key Facts

- 作者构建了 ToolBench，覆盖 16,464 个真实 REST APIs，来自 49 个类别。
- 数据构造分成三步：
  - API collection
  - instruction generation
  - solution path annotation
- 论文提出 ToolLLaMA，并配合 neural API retriever 使用。
- 作者提出 DFSDT（depth-first search-based decision tree）来增强复杂 tool-use 场景中的规划和回退能力。
- 论文还提出 ToolEval，用自动 pass rate 与 win rate 评估 tool-use 结果。
- ToolLLaMA 在复杂工具使用与 unseen APIs 上表现接近 ChatGPT，并对 APIBench 展示了 OOD generalization。

## Tensions / Contradictions

- 这篇工作的核心不是单一模型能力，而是一个完整 harness：数据、检索、规划、执行、评估一起组成能力。
- 它一方面强调 instruction tuning，另一方面又强调仅有 instruction tuning 不够，必须有检索器、搜索策略和 evaluator。
- 因此 ToolLLM 更像一个 tool-use system design 论文，而不是单纯模型论文。

## Links Into Wiki

- [[tool-use-in-llms]] / [../concepts/tool-use-in-llms.md](../concepts/tool-use-in-llms.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
