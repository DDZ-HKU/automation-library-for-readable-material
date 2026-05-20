---
title: Economics and Alignment
aliases:
  - preferences-incentives-and-alignment
  - ai-economics
tags:
  - ai-foundations
  - alignment
  - incentives
  - preferences
updated: 2026-05-05
source_count: 1
status: active
---

# Summary

经济学在当前知识库里的核心价值，不是市场比喻，而是偏好、激励、制度和对齐语言。它帮助我们把“奖励函数怎么写”“RLHF 为什么难”“群体偏好如何聚合”“AI 为什么会奖励黑客”这些问题，从工程现象提升成偏好估计、机制设计、委托—代理和激励相容问题。

## Current Understanding

- 经济学视角最关键的一步，是把“目标函数”重新理解成“偏好与激励设计对象”。
- 这意味着：
  - 奖励函数设计不只是优化技术，而是机制设计问题
  - 偏好学习不只是打分收集，而是效用估计问题
  - 对齐不只是把目标写清楚，而是处理委托—代理与群体偏好聚合问题
- 对当前仓库最有价值的不是一般经济学，而是它与 agent/AGI 的直接连接：
  - RLHF
  - preference modeling
  - multi-agent coordination
  - platform incentives
  - governance
- 它与博弈论、控制论和复杂性科学的分工也应区分：
  - 博弈论管互动结构
  - 控制论管反馈闭环
  - 复杂性科学管系统级后果
  - 经济学管偏好、激励和制度目标

## Evidence

- 主要依据来自 [[path2agi-economics-and-alignment]] / [../sources/path2agi-economics-and-alignment.md](../sources/path2agi-economics-and-alignment.md)。
- 它与 [[game-theory-for-ai-interaction]] / [game-theory-for-ai-interaction.md](game-theory-for-ai-interaction.md) 构成强互补：
  - 一个问互动结构
  - 一个问为什么这些规则会导向特定结果
- 对当前仓库已有主题而言，[[tool-use-in-llms]] / [tool-use-in-llms.md](tool-use-in-llms.md) 和 [[agent-harness-engineering]] / [agent-harness-engineering.md](agent-harness-engineering.md) 已经具备机制设计与反馈约束的原型，只是此前没有显式经济学语言来压缩它们。

## Open Questions

- 如果继续扩 AGI 主题线，最该先补的是机制设计、行为经济学，还是社会选择理论？
- RLHF 在当前仓库里最适合被归为控制问题、经济问题，还是两者共同问题？
- 怎样把“偏好、激励、制度、对齐”进一步压成可迁移的 workflow 或 framework？

## Related Pages

- [[path2agi-economics-and-alignment]] / [../sources/path2agi-economics-and-alignment.md](../sources/path2agi-economics-and-alignment.md)
- [[game-theory-for-ai-interaction]] / [game-theory-for-ai-interaction.md](game-theory-for-ai-interaction.md)
- [[cybernetics]] / [cybernetics.md](cybernetics.md)
- [[tool-use-in-llms]] / [tool-use-in-llms.md](tool-use-in-llms.md)
