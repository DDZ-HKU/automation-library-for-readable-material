---
title: The Annotated Transformer
source_path: raw/The Annotated Transformer.md
source_type: annotated-paper
author: Sasha Rush; Austin Huang; Suraj Subramanian; Jonathan Sum; Khalid Almubarak; Stella Biderman
published: 2022
processed: 2026-04-09
topics:
  - transformers
  - attention
  - sequence-to-sequence-models
  - neural-machine-translation
entities:
  - Sasha Rush
  - Austin Huang
  - Suraj Subramanian
  - Jonathan Sum
  - Khalid Almubarak
  - Stella Biderman
status: active
---

# Summary

这份资料不是原始论文本身，而是对 [[attention-is-all-you-need]] / [attention-is-all-you-need.md](attention-is-all-you-need.md) 的逐段注释与实现说明。它把 Transformer 解释成一种仍保留 encoder-decoder 外形、但完全去掉 RNN/卷积递归路径、改为以 self-attention 和前馈层为核心的序列建模架构。

## Core Claims

- Transformer 继承了 seq2seq 的 encoder-decoder 外框，但抛弃了基于循环状态传播的核心机制。
- self-attention 让任意位置之间的依赖路径长度变成常数级，不再像 RNN 那样必须沿时间步逐层传递。
- 多头注意力不是单纯“多做几次 attention”，而是让模型在不同子空间并行建立不同类型的关系。
- positional encoding 的作用是补回在纯 attention 架构中本来缺失的位置信息。
- 训练层面，残差、layer norm、warmup 学习率调度、label smoothing 等工程设计同样是 Transformer 成功的重要部分。

## Key Facts

- 资料明确对比了 ConvS2S、ByteNet 与 Transformer 在远距离依赖路径长度上的差异。
- 它强调 Transformer 是第一个完全依赖 self-attention 来做输入输出表示计算的主流 transduction 模型。
- 文中代码把模型拆成 `EncoderDecoder`、multi-head attention、position-wise feed-forward、embedding、positional encoding 等清晰模块。
- Decoder 仍是自回归的，但不再通过 recurrent state 递推，而是靠 masked self-attention 读取已生成前缀。
- 这份注释版材料的价值不只在结论，还在把论文中的架构和训练细节展开成可运行实现。

## Tensions / Contradictions

- 资料主要是实现与解释性整理，不等同于原始论文证据本身；它更适合作为理解入口，而不是唯一来源。
- 其中“常数路径长度更利于长程依赖学习”的论点很有解释力，但真实效果仍受头数、上下文长度、分辨率损失与训练规模影响。
- 它代表的是 Transformer 奠基阶段的 encoder-decoder 版本，而不是后来 decoder-only 大语言模型的全部实践。

## Links Into Wiki

- [[attention-is-all-you-need]] / [attention-is-all-you-need.md](attention-is-all-you-need.md)
- [[sequence-to-sequence-for-sets]] / [../concepts/sequence-to-sequence-for-sets.md](../concepts/sequence-to-sequence-for-sets.md)
- [[transformers]] / [../concepts/transformers.md](../concepts/transformers.md)
- [[recurrent-neural-networks]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
