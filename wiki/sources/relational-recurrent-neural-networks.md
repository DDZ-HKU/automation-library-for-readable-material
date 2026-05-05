---
title: Relational Recurrent Neural Networks
source_path: raw/sources/1806.01822v2/1806.01822v2.md
source_type: paper
author: Adam Santoro; Ryan Faulkner; David Raposo; Jack Rae; Mike Chrzanowski; Theophane Weber; Daan Wierstra; Oriol Vinyals; Razvan Pascanu; Timothy Lillicrap
published: 2018
processed: 2026-04-16
topics:
  - recurrent-neural-networks
  - attention
  - relational-reasoning
  - memory-augmented-networks
entities:
  - Adam Santoro
  - Ryan Faulkner
  - David Raposo
  - Jack Rae
  - Mike Chrzanowski
  - Theophane Weber
  - Daan Wierstra
  - Oriol Vinyals
  - Razvan Pascanu
  - Timothy Lillicrap
status: active
---

# Summary

这篇论文提出 Relational Memory Core (RMC)，把 multi-head dot-product attention 放进 recurrent memory 内部，让 memory slots 之间可以直接交互，用来增强 relational reasoning。它的核心判断是：普通循环记忆擅长保存上下文，但不一定擅长让记忆元素彼此比较、组合和推理。

## Core Claims

- 标准 recurrent / memory architectures 更像状态保存器，而不是关系推理器。
- relational reasoning 需要 memory-to-memory interaction，而不只是更长的记忆长度。
- RMC 通过 multi-head attention 让 memory slots 之间直接通信，因此更适合复杂关系任务。
- 这种设计把 attention 从外部读写机制推进成了 memory 内部的关系算子。
- 论文的 guiding design principle 是同时支持信息 compartmentalization 与 compartmentalized information 之间的 interaction。

## Key Facts

- 论文把 RMC 用在 reinforcement learning、program evaluation 和 language modeling 上。
- 报告在 WikiText-103、Project Gutenberg 和 Gigaword 上达到强结果。
- 论文强调在一些关系任务和 RL 任务里，普通 memory network 不够强，RMC 能显著提升表现。
- 模型采用固定数量的 memory slots，并在单个时间步内让这些 memories 彼此做 multi-head dot-product attention。
- 论文还明确把 RMC 与“对所有历史状态做 attention 的 growing buffer 类方法”区分开，强调它是在 recurrent core 内部做关系交互，而不是跨全部历史展开。

## Tensions / Contradictions

- 这篇工作保留了 recurrent 记忆主线，但把真正的瓶颈从“记得住”推进到“会不会关系交互”。
- 因而它是 RNN 向 attention 化、关系化演进的一个过渡点。

## Links Into Wiki

- [[relational-memory-core]] / [../concepts/relational-memory-core.md](../concepts/relational-memory-core.md)
- [[recurrent-neural-networks]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
