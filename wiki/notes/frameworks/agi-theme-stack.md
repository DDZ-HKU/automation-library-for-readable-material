---
title: AGI Theme Stack
updated: 2026-05-06
status: active
---

# Summary

这页把当前仓库里与 AGI 最相关的主题压成一条五层栈，目的是避免把 tool use、harness、控制论、复杂性、博弈论和对齐分别理解成孤立话题。最稳的读法是：先看系统能不能执行，再看它是否形成闭环，再看闭环放大后的整体行为，再看多主体互动结构，最后看系统到底替谁优化。

## Confirmed Understanding

- [[ai-as-cross-disciplinary-convergence]] / [../../concepts/ai-as-cross-disciplinary-convergence.md](../../concepts/ai-as-cross-disciplinary-convergence.md) 已确认，AI/AGI 更适合被理解成跨学科汇流系统，而不是单一模型技术线。
- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md) 已确认，tool use 不是单次 function calling，而是检索、选择、执行、反馈和评估组成的能力链。
- [[agent-harness-engineering]] / [../../concepts/agent-harness-engineering.md](../../concepts/agent-harness-engineering.md) 已确认，agent system 的关键不只是模型，而是外层 harness 对状态、环境、trace、审批和 stop condition 的治理。
- [[cybernetics]] / [../../concepts/cybernetics.md](../../concepts/cybernetics.md) 已确认，反馈闭环是理解 agent、RL、RLHF 和 harness 的统一中层语言。
- [[complexity-science-for-ai-systems]] / [../../concepts/complexity-science-for-ai-systems.md](../../concepts/complexity-science-for-ai-systems.md) 已确认，一旦系统进入大规模、强耦合、多主体或开放环境，问题会从局部能力转成整体行为。
- [[game-theory-for-ai-interaction]] / [../../concepts/game-theory-for-ai-interaction.md](../../concepts/game-theory-for-ai-interaction.md) 已确认，多主体情境下必须引入均衡、对抗、协同和规则设计语言。
- [[economics-and-alignment]] / [../../concepts/economics-and-alignment.md](../../concepts/economics-and-alignment.md) 已确认，奖励、偏好、激励和对齐问题不能只按 loss engineering 理解，而要按偏好估计、机制设计和委托代理结构理解。

## Explicit Knowledge vs Tacit Interpretation

### Explicit Knowledge

- 当前仓库已经有一条从执行能力到制度目标的连续主题线。
- 这条主题线至少包含五层：执行、反馈、整体行为、互动结构、偏好与激励。
- 各层之间不是替代关系，而是解释粒度逐层上移。

### Tacit Interpretation

- AGI 不应被理解成“更强的模型”，而更像“进入环境后的多层系统”。
- 真正的分水岭不是模型参数规模，而是系统何时开始需要治理反馈、生态、互动和激励错配。
- 当前仓库最强的不是认知模拟路线，而是 agent systems 路线：先从 tool use 和 harness 出发，再往上接控制、复杂性、博弈与对齐。

## Layered Stack

### Layer 1: Execution

- 核心页面：[[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md)
- 核心问题：系统会不会做事，能不能稳定调用环境、工具和外部程序。
- 判断信号：tool retrieval、tool selection、多步执行、结果评估是否构成最小能力链。

### Layer 2: Feedback and Harness

- 核心页面：[[agent-harness-engineering]] / [../../concepts/agent-harness-engineering.md](../../concepts/agent-harness-engineering.md)，[[cybernetics]] / [../../concepts/cybernetics.md](../../concepts/cybernetics.md)
- 核心问题：系统是否形成可治理闭环，能否观察状态、比较误差、调整行为并在必要时停止。
- 判断信号：外部状态、trace、verification、approval gate、stop condition 是否成立。

### Layer 3: System-Level Behavior

- 核心页面：[[complexity-science-for-ai-systems]] / [../../concepts/complexity-science-for-ai-systems.md](../../concepts/complexity-science-for-ai-systems.md)
- 核心问题：多个闭环耦合后，系统整体会不会出现涌现、脆弱性、生态反馈或规模跃迁。
- 判断信号：局部看似正常但整体行为失稳，或规模增长后出现不可局部还原的变化。

### Layer 4: Strategic Interaction

- 核心页面：[[game-theory-for-ai-interaction]] / [../../concepts/game-theory-for-ai-interaction.md](../../concepts/game-theory-for-ai-interaction.md)
- 核心问题：当多个主体互相影响时，系统会稳定在什么策略结构上。
- 判断信号：最优动作是否依赖其他主体动作，是否存在对抗、协作、均衡或机制约束。

### Layer 5: Preferences, Incentives, and Alignment

- 核心页面：[[economics-and-alignment]] / [../../concepts/economics-and-alignment.md](../../concepts/economics-and-alignment.md)
- 核心问题：系统到底替谁优化，当前奖励、偏好和制度安排是否会把系统推向错误目标。
- 判断信号：reward hacking、偏好错配、委托代理问题、评价制度反向塑形是否出现。

## How To Apply

看一个 agent / AGI 问题时，不要直接问“模型够不够强”，而是按这条栈往上检查：

1. 先问执行层是否成立：系统是不是连稳定 tool use 都还没完成。
2. 再问反馈层是否成立：它有没有被 harness 组织成可观测、可验证、可停止的闭环。
3. 如果系统已经跨多步、多模块或多主体，再问整体行为层：规模和耦合有没有带来新现象。
4. 如果结果取决于多个主体互相适应，再问互动层：问题是不是已经变成博弈结构。
5. 最后问对齐层：当前被优化的 signal 与真实目标之间有没有激励错配。

一个实用规则是：越往上层走，问题越不像“模型能力不足”，越像“系统结构、互动规则或激励设计出了偏差”。

## To Be Verified

- 当前主题栈主要覆盖 agent systems 路线，对认知科学、语言学和社会治理的高层整合仍不完整。
- 复杂性、博弈论和经济学之间的边界，在真实多智能体系统里可能比当前页面划分更模糊，后续仍需结合新资料继续收束。

## Source Trace

- [[ai-as-cross-disciplinary-convergence]] / [../../concepts/ai-as-cross-disciplinary-convergence.md](../../concepts/ai-as-cross-disciplinary-convergence.md)
- [[cybernetics]] / [../../concepts/cybernetics.md](../../concepts/cybernetics.md)
- [[complexity-science-for-ai-systems]] / [../../concepts/complexity-science-for-ai-systems.md](../../concepts/complexity-science-for-ai-systems.md)
- [[game-theory-for-ai-interaction]] / [../../concepts/game-theory-for-ai-interaction.md](../../concepts/game-theory-for-ai-interaction.md)
- [[economics-and-alignment]] / [../../concepts/economics-and-alignment.md](../../concepts/economics-and-alignment.md)
- [[agent-harness-engineering]] / [../../concepts/agent-harness-engineering.md](../../concepts/agent-harness-engineering.md)
- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md)

## Links

- [[research-reading-and-decision-stack]] / [research-reading-and-decision-stack.md](research-reading-and-decision-stack.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
- [[agent-harness-minimum-architecture]] / [agent-harness-minimum-architecture.md](agent-harness-minimum-architecture.md)
