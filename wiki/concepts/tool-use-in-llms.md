---
title: Tool Use in LLMs
aliases:
  - llm-tool-use
  - tool-using-agents
  - api-using-llms
tags:
  - llm-agents
  - tool-use
  - evaluation
  - retrieval
updated: 2026-04-11
source_count: 1
status: active
---

# Summary

LLM 的 tool use 不是简单的 function calling，而是一整条能力链：工具检索、工具选择、多步规划、真实执行、环境反馈吸收和结果评估。更进一步，这条线还会延伸到 tool making 和 tool library generation。ToolLLM 与 LATM 的价值，就在于把这些环节从“单次调用技巧”推进成一个系统分工问题。

## Current Understanding

- tool-use 的关键困难不只是“模型会不会调用工具”，而是“在大量工具里怎样找对、怎样排对、怎样根据真实返回值继续走”。
- 因此 tool-use 不能被压缩成单步 function call 能力，而更像一个小型 agent loop。
- ToolLLM 说明，真实 tool-use 训练要同时建设：
  - 真实 API 数据
  - instruction tuning
  - 多步 reasoning strategy
  - API retriever
  - evaluator
- 在这个视角里，ToolBench 不只是数据集，而是 tool-use world model 的一部分；ToolEval 不只是评测，而是能力定义的一部分。
- DFSDT 的意义在于：tool-use 不是静态问答，错误路径应该允许回退和重选，因此单路径 ReACT 往往不够。
- 这也说明 tool-use 研究与 agent harness 工程高度相关：一旦环境、工具和评估都进入系统，模型只是其中一个组件。
- LATM 则进一步说明，很多时候真正稀缺的不是“会不会用现成工具”，而是“能不能生成可复用工具并形成 functional cache”。
- CREATOR 则补出另一层：tool creation 本身也需要阶段拆分，尤其要把抽象工具创建与具体决策执行解耦。
- ToolLibGen 则进一步说明，一旦 tool making 成功，新的核心瓶颈会转向“工具如何被聚合、组织和检索”，否则规模化后 retrieval 会先崩。
- API synthesis 方向则提供了另一条相关但不同的路径：不是管理已有工具资产，而是让 LLM 直接综合新的 API 实现。
- 因此，这条线至少可以分成三层：
  - tool use
  - tool making
  - tool library / tool asset reuse
  - 以及一条旁支：api synthesis / program synthesis

## Evidence

- 主要依据来自 [[toolllm-facilitating-large-language-models-to-master-16000-real-world-apis]] / [../sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md](../sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md)。
- 关于 LLM 如何进入 tool making / functional cache 结构，补充来自 [[large-language-models-as-tool-makers]] / [../sources/large-language-models-as-tool-makers.md](../sources/large-language-models-as-tool-makers.md)。
- 关于 tool creation 中 abstract reasoning 与 concrete decision 的解耦，补充来自 [[creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models]] / [../sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md](../sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md)。
- 关于如何把大量 question-specific tools 重构成可检索的 structured tool library，补充来自 [[toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning]] / [../sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md](../sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md)。
- 关于 LLM 直接综合 API 实现的 synthesis 路径，补充来自 [[an-approach-for-api-synthesis-using-large-language-models]] / [../sources/an-approach-for-api-synthesis-using-large-language-models.md](../sources/an-approach-for-api-synthesis-using-large-language-models.md)。
- 与 [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md) 对照看，ToolLLM 恰好证明了 harness 不是附属层，而是能力本身的一部分。

## Open Questions

- 在 tool-use 场景里，真正的瓶颈主要是模型 reasoning、retriever 质量，还是 evaluator 设计？
- 大规模真实 API 训练与更抽象的 tool creation / tool synthesis 之间，应如何建立更清晰的关系？
- 在 tool creation 阶段，抽象 reasoning 与具体 decision 应该怎样分层，才能提高稳定性？
- ToolLLM 之后，哪些工作真正解决了“无限正确路径”下的评估难题？
- 当工具可以被模型自己生成后，工具使用与工具生成之间的最佳分工边界在哪里？
- 当工具规模化增长后，真正的系统瓶颈是不是会从“tool creation”转移到“tool organization and retrieval”？
- API synthesis 与 tool creation 的边界在哪里？什么时候应当让模型“造工具”，什么时候应当让它“综合 API 实现”？

## Related Pages

- [[toolllm-facilitating-large-language-models-to-master-16000-real-world-apis]] / [../sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md](../sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md)
- [[large-language-models-as-tool-makers]] / [../sources/large-language-models-as-tool-makers.md](../sources/large-language-models-as-tool-makers.md)
- [[creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models]] / [../sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md](../sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md)
- [[toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning]] / [../sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md](../sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md)
- [[an-approach-for-api-synthesis-using-large-language-models]] / [../sources/an-approach-for-api-synthesis-using-large-language-models.md](../sources/an-approach-for-api-synthesis-using-large-language-models.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
