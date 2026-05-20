---
title: Game Theory for AI Interaction
aliases:
  - ai-game-theory
  - strategic-interaction-in-ai
tags:
  - ai-foundations
  - game-theory
  - multi-agent
  - alignment
updated: 2026-05-05
source_count: 1
status: active
---

# Summary

博弈论在当前知识库里的主要作用，是把 AI 从单主体优化带到多主体策略性交互。它给我们一套稳定性、对抗性与机制约束的语言，适合解释 self-play、多智能体 RL、对抗训练，以及 agent 系统进入人与系统、系统与系统互动后的策略结构。

## Current Understanding

- 只要一个系统的最优动作取决于其他主体的动作，问题就不再只是优化，而开始进入博弈。
- 对当前仓库最有用的不是博弈论的全部数学细节，而是几类核心判断：
  - 均衡能否稳定
  - 对抗是否可避免
  - 规则设计是否会改变结果
- 这个视角可以直接接到现有仓库里的几条线：
  - tool-use 与 tool-selection 的竞争/协调结构
  - multi-agent workflows
  - RLHF 和 alignment 的激励结构
  - 对抗训练与鲁棒性
- 它与经济学的关系也要分清：
  - 博弈论更擅长刻画互动结构与均衡
  - 经济学进一步补偏好、制度和激励设计

## Evidence

- 主要依据来自 [[path2agi-game-theory]] / [../sources/path2agi-game-theory.md](../sources/path2agi-game-theory.md)。
- 它与 [[economics-and-alignment]] / [economics-and-alignment.md](economics-and-alignment.md) 形成上下游关系：
  - 一个处理互动结构
  - 一个处理偏好与制度目标
- 它与 [[complexity-science-for-ai-systems]] / [complexity-science-for-ai-systems.md](complexity-science-for-ai-systems.md) 也互补：
  - 一个更偏策略分析
  - 一个更偏整体行为

## Open Questions

- 对当前仓库最该补的，是均衡与机制设计，还是算法博弈论与计算复杂性？
- 在 agent 系统里，多主体 interaction 的主要瓶颈是激励、通信，还是反馈速度？
- 哪些现有 outputs 最应该被回读成博弈结构，而不仅是执行结构？

## Related Pages

- [[path2agi-game-theory]] / [../sources/path2agi-game-theory.md](../sources/path2agi-game-theory.md)
- [[economics-and-alignment]] / [economics-and-alignment.md](economics-and-alignment.md)
- [[complexity-science-for-ai-systems]] / [complexity-science-for-ai-systems.md](complexity-science-for-ai-systems.md)
- [[tool-use-in-llms]] / [tool-use-in-llms.md](tool-use-in-llms.md)
