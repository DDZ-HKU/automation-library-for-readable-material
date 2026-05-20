---
title: Cybernetics
aliases:
  - control-theory-for-intelligent-systems
  - feedback-systems
tags:
  - ai-foundations
  - control
  - feedback
  - agents
updated: 2026-05-05
source_count: 1
status: active
---

# Summary

控制论为智能系统提供了“反馈”的通用语言：系统如何感知状态、比较目标与现实、再根据误差调整行为。对当前仓库来说，它最有价值的不是复习经典控制理论，而是提供一个统一视角去理解 agent、强化学习、RLHF、harness feedback loops 以及“humans steer, agents execute”这类工程结构。

## Current Understanding

- 控制论最核心的抽象是闭环：观察、比较、调整。
- 这个闭环能帮助我们把很多现代 AI 现象放回同一语言里：
  - 梯度下降是参数层反馈
  - 强化学习是策略层反馈
  - RLHF 是偏好层反馈
  - harness engineering 是环境与验证层反馈
- 因此，控制论不是“旧学科旁支”，而是理解智能体系统为何需要状态、边界、传感器和停止条件的一个底层框架。
- 从当前仓库的视角看，控制论最直接补上的不是数学细节，而是一个中层判断模板：
  - 什么时候一个系统还是静态模型
  - 什么时候它已经变成必须治理反馈回路的 agent system
- 这也解释了为什么当前仓库里的 harness 主题线与 tool-use 主题线会自然汇合：一旦模型进入工具环境，反馈质量与控制结构就会变成能力本身的一部分。

## Evidence

- 主要依据来自 [[path2agi-cybernetics]] / [../sources/path2agi-cybernetics.md](../sources/path2agi-cybernetics.md)。
- 与当前仓库现有知识对照看，[[agent-harness-engineering]] / [agent-harness-engineering.md](agent-harness-engineering.md) 已经把环境、状态、trace、verification 和 stop condition 组织成工程 feedback system。
- [[tool-use-in-llms]] / [tool-use-in-llms.md](tool-use-in-llms.md) 也已确认，tool use 更像检索、选择、执行、反馈、评估的闭环，而不是单步 function call。

## Open Questions

- 控制论与当前仓库里的 harness engineering 之间，最有迁移价值的共同中介变量是什么：状态、反馈速度、传感器质量，还是 stop condition？
- 对 agent 系统来说，控制论框架在哪里仍然过于抽象，必须补上认知、语言或组织层解释？
- 如果继续补 Path2AGI 相关内容，下一步最该补的是复杂性科学、运筹学，还是博弈论？

## Related Pages

- [[path2agi-cybernetics]] / [../sources/path2agi-cybernetics.md](../sources/path2agi-cybernetics.md)
- [[ai-as-cross-disciplinary-convergence]] / [ai-as-cross-disciplinary-convergence.md](ai-as-cross-disciplinary-convergence.md)
- [[agent-harness-engineering]] / [agent-harness-engineering.md](agent-harness-engineering.md)
- [[tool-use-in-llms]] / [tool-use-in-llms.md](tool-use-in-llms.md)
