---
title: GPipe: Easy Scaling with Micro-Batch Pipeline Parallelism
source_path: raw/sources/1811.06965v5/1811.06965v5.md
source_type: paper
author: Yanping Huang; Youlong Cheng; Ankur Bapna; Orhan Firat; Mia Xu Chen; Dehao Chen; HyoukJoong Lee; Jiquan Ngiam; Quoc V. Le; Yonghui Wu; Zhifeng Chen
published: 2018
processed: 2026-04-09
topics:
  - transformers
  - model-parallelism
  - pipeline-parallelism
  - scaling-laws
entities:
  - Yanping Huang
  - Quoc V. Le
  - Yonghui Wu
status: active
---

# Summary

这篇论文讨论的不是新的 Transformer 结构，而是如何把非常大的神经网络真正训练起来。核心贡献是 GPipe：一种基于 micro-batch 的 pipeline parallelism 方法，它把顺序层切分到多台加速器上，并用同步梯度更新来避免异步流水线带来的权重陈旧问题。

## Core Claims

- 当模型大到单个加速器放不下时，关键问题不再只是“架构更强”，而是如何高效做模型并行。
- GPipe 适用于任何能表示成层序列的网络，因此不局限于 Transformer，也可用于大规模卷积网络。
- 将 mini-batch 切分成多个 micro-batches，再在不同设备间做流水线执行，可以显著提高设备利用率。
- 通过在整个 mini-batch 结束后做一次同步梯度更新，GPipe 避免了异步 pipeline 方法中的权重陈旧问题。
- 配合 re-materialization，GPipe 能用额外计算换取显著更低的激活内存占用。

## Key Facts

- 论文报告了一个 128 层、约 60 亿参数的多语言 Transformer，覆盖 100 多种语言。
- GPipe 的接口强调三个核心控制量：分区数 `K`、micro-batch 数 `M`、以及按顺序定义的层列表。
- 论文把流水线中的 idle time 概括为 bubble overhead，并指出当 `M >= 4K` 时这一开销通常较小。
- 与 SPMD / Mesh-TensorFlow 相比，GPipe 的跨设备通信主要发生在分区边界，因此通信模式更简单。
- 与 PipeDream 相比，GPipe 牺牲了一部分异步激进性，换来同步更新和更稳定的一致训练语义。

## Tensions / Contradictions

- GPipe 解决的是“如何扩大模型”而不是“为什么 Transformer 有效”，所以它属于训练基础设施层，而非表示学习层。
- 它假设单层本身仍能装入单个加速器内存，因此并不能覆盖所有极端超大层场景。
- pipeline parallelism 减少了部分通信压力，但也引入了分区均衡、bubble overhead 和 micro-batch 设计等新工程权衡。

## Links Into Wiki

- [[transformers]] / [../concepts/transformers.md](../concepts/transformers.md)
- [[pipeline-parallelism]] / [../concepts/pipeline-parallelism.md](../concepts/pipeline-parallelism.md)
