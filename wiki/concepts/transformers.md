---
title: Transformers
aliases:
  - transformer
  - self-attention-models
tags:
  - deep-learning
  - sequence-modeling
  - attention
updated: 2026-04-09
source_count: 5
status: active
---

# Summary

Transformer 是 seq2seq 演化中的一次范式转移：它保留了 encoder-decoder 的整体任务接口，但不再依赖 RNN/LSTM 那种沿时间步压缩并传递隐藏状态的方式，而是改用 self-attention 直接在位置之间建立信息访问。

## Current Understanding

- Transformer 的核心断点不只是“用了 attention”，而是把 attention 从辅助机制提升成主要的表示与依赖建模机制。
- 与 Bahdanau attention 相比，Transformer 的更大变化不是“第一次有 attention”，而是第一次让 attention 不再依附于 recurrent encoder-decoder 主路径。
- 在 RNN/LSTM 中，远距离信息通常必须穿过一条顺序状态链传播；在 Transformer 中，不同位置可以通过 attention 直接交互。
- 这种设计带来两个直接后果：训练并行性更强，以及长程依赖不再完全受制于 recurrent path 的长度。
- 纯 attention 架构丢失了天然的顺序归纳偏置，因此需要 positional encoding 或其他位置机制补回位置信息。
- 多头注意力让模型可以在多个关系子空间里并行建模，而不是只做单一相似度匹配。
- Transformer 仍属于自回归条件分解家族的一员；变化的是“如何访问上下文”，而不是彻底放弃 next-token / next-symbol 预测。
- 当 Transformer 规模继续扩大后，问题会从“架构如何替代 RNN”延伸到“如何把更深更大的 Transformer 稳定训练起来”，这时训练系统和并行策略开始成为核心瓶颈。
- 从原始论文看，Transformer 的主张不是“attention 很有用”，而是“sequence transduction 可以完全不依赖 recurrence 与 convolution”。

## Evidence

- 原始架构主张与实验依据来自 [[attention-is-all-you-need]] / [../sources/attention-is-all-you-need.md](../sources/attention-is-all-you-need.md)。
- attention 作为 pre-Transformer 桥梁机制的起点，来自 [[neural-machine-translation-by-jointly-learning-to-align-and-translate]] / [../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md](../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md)。
- 注释版实现与解释入口来自 [[the-annotated-transformer]] / [../sources/the-annotated-transformer.md](../sources/the-annotated-transformer.md)。
- 关于超大 Transformer 如何借助模型并行继续扩展，补充来自 [[gpipe-easy-scaling-with-micro-batch-pipeline-parallelism]] / [../sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md](../sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md)。
- 与 [[sequence-to-sequence-for-sets]] / [sequence-to-sequence-for-sets.md](sequence-to-sequence-for-sets.md) 结合看，Transformer 可以被理解为 attention 从“集合读取补丁”升级为“主架构”的下一步。
- 与 [[recurrent-neural-networks]] / [recurrent-neural-networks.md](recurrent-neural-networks.md) 对照看，它针对的是顺序计算、长路径依赖和状态压缩瓶颈。
- 与 [[attention-mechanisms]] / [attention-mechanisms.md](attention-mechanisms.md) 对照看，Transformer 是从“每步生成时看一遍源句”进一步走向“整层表示计算都由 attention 组织”。

## Open Questions

- Transformer 真正替代的是 RNN 的“记忆机制”、`seq2seq` 外壳，还是“通过递归状态访问上下文”的那套路径结构？
- 在什么问题上，Transformer 的优势主要来自并行训练；在什么问题上，主要来自信息访问方式本身？
- 从 encoder-decoder Transformer 到 decoder-only LLM，中间最关键的结构与训练目标转折点是什么？
- 如果从今天回看，哪些 RNN 的优势其实只是因为当时 attention 机制还不成熟？
- 在大规模训练层面，Transformer 的扩展瓶颈首先来自内存、通信还是优化稳定性？

## Related Pages

- [[the-annotated-transformer]] / [../sources/the-annotated-transformer.md](../sources/the-annotated-transformer.md)
- [[attention-is-all-you-need]] / [../sources/attention-is-all-you-need.md](../sources/attention-is-all-you-need.md)
- [[neural-machine-translation-by-jointly-learning-to-align-and-translate]] / [../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md](../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md)
- [[attention-mechanisms]] / [attention-mechanisms.md](attention-mechanisms.md)
- [[gpipe-easy-scaling-with-micro-batch-pipeline-parallelism]] / [../sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md](../sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md)
- [[pipeline-parallelism]] / [pipeline-parallelism.md](pipeline-parallelism.md)
- [[sequence-to-sequence-for-sets]] / [sequence-to-sequence-for-sets.md](sequence-to-sequence-for-sets.md)
- [[recurrent-neural-networks]] / [recurrent-neural-networks.md](recurrent-neural-networks.md)
