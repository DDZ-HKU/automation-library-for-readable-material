---
title: Attention Is All You Need
source_path: raw/sources/1706.03762v7/1706.03762v7.md
source_type: paper
author: Ashish Vaswani; Noam Shazeer; Niki Parmar; Jakob Uszkoreit; Llion Jones; Aidan N. Gomez; Lukasz Kaiser; Illia Polosukhin
published: 2017
processed: 2026-04-09
topics:
  - transformers
  - attention
  - sequence-to-sequence-models
  - neural-machine-translation
entities:
  - Ashish Vaswani
  - Noam Shazeer
  - Niki Parmar
  - Jakob Uszkoreit
  - Llion Jones
  - Aidan N. Gomez
  - Lukasz Kaiser
  - Illia Polosukhin
status: active
---

# Summary

这篇论文是 Transformer 的原始提出材料。它的核心贡献不是“在 seq2seq 里再多加一个 attention 模块”，而是直接去掉 recurrence 和 convolution，把 self-attention 提升为输入输出表示计算的主要机制，从而同时改变了长程依赖路径和训练并行性。

## Core Claims

- 序列转导不必以 RNN 或卷积为核心，完全可以只依赖 attention 机制。
- self-attention 将任意两个位置之间的依赖路径缩短到常数级，这对长程依赖学习和并行训练都很关键。
- Multi-head attention 的作用不只是增加容量，而是允许模型在不同表示子空间里并行建模不同关系。
- positional encoding 是纯 attention 架构中补回顺序信息的必要组件之一。
- Transformer 在机器翻译上不仅效果更好，而且训练成本显著低于此前最强模型。

## Key Facts

- 论文明确把旧主流方法概括为“encoder-decoder + recurrent/convolution + attention”。
- 它提出 Transformer encoder-decoder 架构，包含多头自注意力、位置前馈层、残差连接、layer norm 和位置编码。
- 文中强调 recurrent computation 的顺序性会限制并行训练，并把这点作为替换 RNN 的关键动机之一。
- 原文专门比较了 self-attention、recurrent layer 和 convolution layer 的计算复杂度、顺序操作数和最大路径长度。
- 论文报告了 WMT 2014 英德、英法翻译任务上的强结果，并给出了 warmup 学习率、label smoothing、dropout 等训练细节。

## Tensions / Contradictions

- 论文把 self-attention 的常数路径长度作为关键优势之一，但也承认它会带来 attention averaging 的分辨率问题。
- 它代表的是 encoder-decoder Transformer 的原始形态，而不是后来 decoder-only 大语言模型的完整实践。
- 原文里的成功既来自架构变化，也来自较完整的训练配方；阅读时不能把所有收益都简单归因于 attention 本身。

## Links Into Wiki

- [[transformers]] / [../concepts/transformers.md](../concepts/transformers.md)
- [[the-annotated-transformer]] / [the-annotated-transformer.md](the-annotated-transformer.md)
- [[recurrent-neural-networks]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
