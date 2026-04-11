---
title: Attention Mechanisms
aliases:
  - attention
  - bahdanau-attention
  - soft-alignment
tags:
  - deep-learning
  - sequence-modeling
  - attention
  - neural-machine-translation
updated: 2026-04-09
source_count: 3
status: active
---

# Summary

attention 的核心价值，是把模型访问上下文的方式从“先全部压缩，再统一读取”改成“在当前预测步骤上按需读取相关部分”。在当前知识库里，它首先表现为 RNN seq2seq 内部的 soft alignment 机制，随后才被 Transformer 推进为主要架构。

## Current Understanding

- Bahdanau attention 的直接动机，是修复 encoder-decoder 把整句压成 fixed-length vector 带来的信息瓶颈。
- 在这个阶段，attention 不是用来替代 RNN，而是给 decoder 增加一个可微的检索接口，让它在生成每个目标词时重新查看源句。
- attention 的关键变化不是“加权平均”本身，而是 context vector 从全句唯一，变成了随目标位置变化的动态上下文。
- 这说明 pre-Transformer 阶段真正被松动的，是状态压缩假设，而不是整个 seq2seq 外形。
- 到 [[transformers]] / [transformers.md](transformers.md) 阶段，attention 从辅助读取机制升级为主要计算路径，RNN 的递归状态链才被整体移除。
- 从 [[sequence-to-sequence-for-sets]] / [sequence-to-sequence-for-sets.md](sequence-to-sequence-for-sets.md) 回看，attention 还同时承担了另一种作用：为非天然序列对象提供更灵活的集合读取方式。
- 因此，attention 这条线真正连接的是三类问题：长句信息瓶颈、顺序化偏置，以及上下文访问路径长度。

## Evidence

- Bahdanau attention 的起点来自 [[neural-machine-translation-by-jointly-learning-to-align-and-translate]] / [../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md](../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md)。
- attention 作为集合读取机制的中间形态，来自 [[order-matters-sequence-to-sequence-for-sets]] / [../sources/order-matters-sequence-to-sequence-for-sets.md](../sources/order-matters-sequence-to-sequence-for-sets.md)。
- attention 升级为主架构的证据来自 [[attention-is-all-you-need]] / [../sources/attention-is-all-you-need.md](../sources/attention-is-all-you-need.md)。

## Open Questions

- 在 Bahdanau attention 到 Transformer 之间，哪几步工作最关键地把 cross-attention 扩展成 self-attention 主导的统一架构？
- 对很多任务来说，attention 的主要收益究竟来自更短的信息路径，还是来自不必再把全局信息塞进固定状态？
- 哪些任务仍更适合“RNN + attention”式局部修补，而不是完全 attention-first 的架构？
- 如果把 today 的长上下文模型视角带回去，应该如何重新理解这条 attention 演化线？

## Related Pages

- [[neural-machine-translation-by-jointly-learning-to-align-and-translate]] / [../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md](../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md)
- [[recurrent-neural-networks]] / [recurrent-neural-networks.md](recurrent-neural-networks.md)
- [[sequence-to-sequence-for-sets]] / [sequence-to-sequence-for-sets.md](sequence-to-sequence-for-sets.md)
- [[transformers]] / [transformers.md](transformers.md)
- [[attention-is-all-you-need]] / [../sources/attention-is-all-you-need.md](../sources/attention-is-all-you-need.md)
