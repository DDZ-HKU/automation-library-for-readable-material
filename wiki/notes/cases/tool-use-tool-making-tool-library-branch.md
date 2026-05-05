---
title: Tool Use to Tool Making to Tool Library Branch
updated: 2026-04-11
status: active
---

# Summary

`ToolLLM -> CREATOR/LATM -> ToolLibGen` 这条主线真正说明的，不是“工具越来越多”，而是 LLM agent 系统中的瓶颈在不断上移：先是不会用工具，然后是没有合适工具，再然后是工具太多却无法有效组织。与此同时，`API synthesis` 这类工作又提醒我们：相关问题并不全都落在同一主线上，某些论文更接近 program synthesis 旁支。

## Confirmed Understanding

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md) 已确认，ToolLLM 把 tool use 系统化为数据、检索、规划、执行和评估的完整链条。
- 同一概念页也确认，CREATOR 与 LATM 把问题继续推进到 tool making，但关注点不同：CREATOR 强调 creation / decision 的认知分层，LATM 强调 maker / user 的 serving 分工。
- 现在 ToolLibGen 又进一步表明，当 question-specific tools 大量增长后，新的瓶颈变成 tool organization 和 retrieval scaling。
- 同时，API synthesis 工作又表明，并非所有“工具相关论文”都进入这条主线；有些更接近 program synthesis 路径。

## Tacit Interpretation

- 这条线最重要的不是每篇论文分别做了什么，而是它们展示了瓶颈转移规律。
- 当一个 agent 系统刚起步时，最缺的是“会不会调工具”。
- 当它会调工具后，最缺的是“有没有合适工具可调”。
- 当它能生成工具后，最缺的是“这些工具怎样被组织、检索、聚合，而不变成垃圾堆”。
- 这说明 agent 工程的成熟路径，往往不是单一模型越来越强，而是：
  - action
  - asset creation
  - asset management
  这三层逐步分化。
- 但相关领域还会分叉出 synthesis 旁支，所以做知识库整理时要注意：不要把所有“工具”“API”“代码生成”论文粗暴压成一条线。

## What This Teaches

- 只盯着 function calling 会低估 tool-use 系统真正的后续复杂性。
- 真正的长期问题常常不是“会不会生成”，而是“生成之后如何管理”。
- 所以 tool-use 分支不能只看 agent prompt 或单次任务成败，还要看：
  - retriever
  - evaluator
  - cache
  - library structure
  - tool governance

## How To Think

遇到 agent/tool 论文时，可以先问：

1. 这篇主要在解决 use、make，还是 organize？
2. 它的真正瓶颈是单次推理，还是长期资产管理？
3. 它是增加模型能力，还是增加系统结构？

## How To Apply

- 当前这条 tool 分支下一步最该补的，不是再找一篇泛泛的 function-calling 论文，而是继续沿：
  - tool retrieval
  - tool evaluation
  - tool governance
  这几条系统问题补关键断点
- 同时应单独维护一条 `API synthesis / program synthesis` 的旁支，而不是把它硬塞进 tool governance 主线。

## Links

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md)
- [[toolllm-facilitating-large-language-models-to-master-16000-real-world-apis]] / [../../sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md](../../sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md)
- [[creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models]] / [../../sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md](../../sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md)
- [[large-language-models-as-tool-makers]] / [../../sources/large-language-models-as-tool-makers.md](../../sources/large-language-models-as-tool-makers.md)
- [[toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning]] / [../../sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md](../../sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md)
- [[an-approach-for-api-synthesis-using-large-language-models]] / [../../sources/an-approach-for-api-synthesis-using-large-language-models.md](../../sources/an-approach-for-api-synthesis-using-large-language-models.md)
