---
title: Large Language Models as Tool Makers
source_path: raw/sources/2305.17126v2/2305.17126v2.md
source_type: paper
author: Tianle Cai; Xuezhi Wang; Tengyu Ma; Xinyun Chen; Denny Zhou
published: 2023
processed: 2026-04-11
topics:
  - tool-making
  - llm-agents
  - tool-use
  - serving
entities:
  - Tianle Cai
  - Xuezhi Wang
  - Tengyu Ma
  - Xinyun Chen
  - Denny Zhou
  - LATM
status: active
---

# Summary

这篇论文提出 `LLMs As Tool Makers (LATM)`。它的核心推进不再是让 LLM “学会使用已有工具”，而是让 LLM 进入一个 closed-loop：高能力模型负责造可复用工具，较便宜模型负责调用这些工具，从而同时提升能力和降低平均 serving cost。

## Core Claims

- 现有 tool-using 方法受限于“是否已经有合适工具可用”，而这本身是瓶颈。
- 因此更进一步的方向是让 LLM 自己生成 reusable tools，而不只是调用固定工具。
- `tool making` 与 `tool using` 应当分成两个阶段，由不同能力/成本档位的模型承担。
- 这种两阶段结构本质上形成了一种 *functional cache*：缓存的不是自然语言答案，而是可复用功能。
- 在多次相似请求场景下，这种结构可以把高能力模型的一次性造工具成本，摊到后续大量低成本调用上。

## Key Facts

- LATM 把系统分成：
  - tool maker
  - tool user
- 工具被实现为 Python utility function，并可在后续请求中复用。
- 作者明确把这看成一种 cost-performance tradeoff：GPT-4 可做 tool maker，GPT-3.5 可做 tool user。
- 论文强调 functional cache 相比传统 response cache 的关键差别：缓存的是“功能”，不是“文字回答”。
- 在 Big-Bench 等复杂任务上，GPT-4 做 maker、GPT-3.5 做 user 可达到接近双 GPT-4 的性能，但成本更低。

## Tensions / Contradictions

- 这篇工作的核心不是更强的单次推理，而是“把能力前置为可复用工件”，因此它更像 serving architecture 论文。
- 它和 ToolLLM 的关注点不同：ToolLLM 更关心 open-source LLM 如何掌握大量真实 API；LATM 更关心工具本身由谁生成、如何复用、如何降成本。
- 因此 LATM 更接近“tool creation / functional caching”线，而不是纯粹“tool use benchmark”线。

## Links Into Wiki

- [[tool-use-in-llms]] / [../concepts/tool-use-in-llms.md](../concepts/tool-use-in-llms.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
