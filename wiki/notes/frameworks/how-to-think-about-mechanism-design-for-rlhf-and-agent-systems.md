---
title: How to Think About Mechanism Design for RLHF and Agent Systems
updated: 2026-05-06
status: active
---

# Summary

把 RLHF 或 agent alignment 看成“奖励函数调参”会低估问题难度。更稳的视角是把它看成机制设计问题：你不是在给一个被动模型写 loss，而是在设计一套规则，让一个会适应激励的代理尽量产生你真正想要的行为。

## Confirmed Understanding

- [[economics-and-alignment]] / [../../concepts/economics-and-alignment.md](../../concepts/economics-and-alignment.md) 已确认，奖励函数设计更像 incentive design，而不是单纯 optimization。
- [../../../outputs/economics-and-alignment-for-rlhf-and-agents-2026-05-06.md](../../../outputs/economics-and-alignment-for-rlhf-and-agents-2026-05-06.md) 已确认，reward hacking、表面顺从和 grader 迎合，都是“规则被利用”的自然结果。
- [[game-theory-for-ai-interaction]] / [../../concepts/game-theory-for-ai-interaction.md](../../concepts/game-theory-for-ai-interaction.md) 已确认，一旦代理的最优策略取决于评价者、平台或其他代理，问题就进入策略性交互结构。

## The Core Reframe

机制设计最重要的一步，是把问题从：

- “这个目标函数该怎么写？”

改写成：

- “什么规则会让代理在追求自身最优时，仍然更接近我的真实目标？”

这里最关键的不是奖励值本身，而是：

- 代理观察到什么信号
- 什么行为会被奖励
- 什么行为会被惩罚
- 什么漏洞最容易被利用

## Four Questions

看一个 RLHF 或 agent system 时，优先问：

1. 谁是 principal？
2. agent 实际在最大化什么 signal？
3. 这个 signal 和真实目标之间有哪些错配空间？
4. 当前机制是否鼓励表面顺从而不鼓励真实目标达成？

## Common Failure Modes

### 1. Reward Hacking

代理学会最大化代理指标，而不最大化真实目标。

### 2. Grader Gaming

代理学会看起来像高分答案，而不是真的更有帮助、更诚实或更安全。

### 3. Proxy Collapse

本来只是临时代理指标的 signal，逐渐被当成了目标本身。

### 4. Incentive Drift

随着部署环境、评估规则或组织流程变化，原本勉强合理的机制开始系统性鼓励错误行为。

## How To Apply

设计奖励或评价机制时，不要只问“能不能训练起来”，还要问：

- 这个规则最容易被怎样利用？
- 如果代理越来越强，漏洞会不会被放大？
- 有没有把“易评分”误当成“真实有价值”？
- 哪些行为值得引入 approval gate，而不是继续细化奖励？

## Rule of Thumb

**好的机制设计不是让代理更难犯错，而是让“做对的事”比“钻规则空子”更有利。**

## Source Trace

- [[economics-and-alignment]] / [../../concepts/economics-and-alignment.md](../../concepts/economics-and-alignment.md)
- [[game-theory-for-ai-interaction]] / [../../concepts/game-theory-for-ai-interaction.md](../../concepts/game-theory-for-ai-interaction.md)
- [../../../outputs/economics-and-alignment-for-rlhf-and-agents-2026-05-06.md](../../../outputs/economics-and-alignment-for-rlhf-and-agents-2026-05-06.md)

## Links

- [[agi-theme-stack]] / [agi-theme-stack.md](agi-theme-stack.md)
- [[how-to-think-about-social-choice-for-alignment-governance]] / [how-to-think-about-social-choice-for-alignment-governance.md](how-to-think-about-social-choice-for-alignment-governance.md)
- [[how-to-think-about-behavioral-economics-for-human-feedback]] / [how-to-think-about-behavioral-economics-for-human-feedback.md](how-to-think-about-behavioral-economics-for-human-feedback.md)
