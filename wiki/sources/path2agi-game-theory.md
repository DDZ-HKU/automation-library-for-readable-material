---
title: Path2AGI on Game Theory
source_path: raw/sources/path2agi-core/22-game-theory.md
source_type: topic-essay
author: Path2AGI repository
published: 2026-04-08
processed: 2026-05-05
topics:
  - game-theory
  - multi-agent
  - strategic-interaction
  - alignment
entities:
  - John Nash
  - John von Neumann
  - Oskar Morgenstern
status: active
---

# Summary

这篇博弈论专题页的核心作用，是把 AI 从“单主体优化”扩展到“多主体策略性交互”。它帮助我们理解：当其他智能体、用户、平台或对手的策略会反过来影响系统时，纳什均衡、极小化极大、机制设计和信息不完全博弈就进入了 AI 主线。

## Core Claims

- 单主体优化不足以描述现实智能系统；许多 AI 场景本质上是策略性交互。
- 博弈论提供了多主体系统的稳定性语言：
  - 纳什均衡
  - 极小化极大
  - 子博弈完美均衡
  - 贝叶斯博弈
- GAN、自我博弈训练、多智能体 RL、对抗鲁棒性和部分对齐问题都可以放回博弈论框架理解。
- 机制设计是博弈论与经济学之间的关键桥：它把“多主体会怎么互相影响”进一步推进成“怎样设规则让结果更可取”。

## Key Facts

- 文章从 Borel、von Neumann、Nash 一直写到算法博弈论和 GAN、自我对弈、RLHF 的现代应用。
- 文章明确指出：
  - 纳什均衡为系统稳定性提供了分析框架
  - 极小化极大定理解释对抗搜索与对抗训练
  - 机制设计为对齐和激励设计提供桥梁
- AI 中的典型落点包括：
  - 多智能体强化学习
  - 对抗训练
  - AlphaGo / AlphaZero 的 self-play
  - RLHF 的机制分析

## Useful Quotes Or Data

- “博弈论将 AI 从‘单智能体优化’扩展到‘多智能体战略交互’。”
- “一个智能体的最优策略取决于其他智能体的策略。”

## Tensions / Contradictions

- 博弈论擅长刻画互动结构与稳定性，但不直接回答偏好来自哪里、制度目标该如何选，这需要经济学进一步补上。
- 用均衡语言理解 AI 很有力量，但现实系统未必真的收敛到理想均衡。
- 文章强调多主体策略性，这对 agent 生态很重要；但真正部署系统时，仍要结合复杂性和控制视角来理解动态演化与反馈速度。

## Links Into Wiki

- [[game-theory-for-ai-interaction]] / [../concepts/game-theory-for-ai-interaction.md](../concepts/game-theory-for-ai-interaction.md)
- [[economics-and-alignment]] / [../concepts/economics-and-alignment.md](../concepts/economics-and-alignment.md)
- [[complexity-science-for-ai-systems]] / [../concepts/complexity-science-for-ai-systems.md](../concepts/complexity-science-for-ai-systems.md)
