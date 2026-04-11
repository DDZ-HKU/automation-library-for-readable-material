---
title: Recurrent Neural Network Regularization
source_path: raw/Obsidian.pdf.md
source_type: paper
author: Wojciech Zaremba; Ilya Sutskever; Oriol Vinyals
published: 2015
processed: 2026-04-08
topics:
  - recurrent-neural-networks
  - lstm
  - dropout
  - regularization
entities:
  - Wojciech Zaremba
  - Ilya Sutskever
  - Oriol Vinyals
status: active
---

# Summary

这篇论文讨论了如何把 dropout 正确用于 LSTM：核心结论不是“给所有连接都加 dropout”，而是只在非循环连接上使用 dropout，这样既能减少过拟合，又不会破坏 LSTM 记忆长程信息的能力。

## Core Claims

- 传统 dropout 直接用于 RNN/LSTM 效果不好，主要因为循环连接上的噪声会破坏时序记忆。
- 一个简单有效的方案是只对非循环连接施加 dropout，而保留 recurrent connections 不受 dropout 扰动。
- 这种做法能显著降低 LSTM 在多个任务上的过拟合。
- 论文在语言建模、语音识别、机器翻译和图像描述上都观察到性能提升。

## Key Facts

- 论文研究对象是带 LSTM 单元的深层 RNN。
- 作者强调，大模型 RNN 往往受过拟合限制，而不是表达能力不足。
- 在 PTB 词级语言建模上，regularized LSTM 相比 non-regularized LSTM 显著降低 perplexity。
- 论文中的直觉解释是：信息沿时间传播时，不应在 recurrent path 上被反复随机破坏。
- 文章把 dropout 施加在层间或输出方向的非循环通路上，使信息跨时间传播的主要记忆路径更稳定。

## Tensions / Contradictions

- 论文给出的是当时 LSTM 训练中的关键经验法则，但后续文献还发展出了 variational dropout、recurrent dropout 等更细分方案。
- 结果跨多个任务有效，但这里的论证仍主要是工程经验与实验验证，而非一般性理论证明。
- 从今天视角看，这属于 pre-Transformer 时代的序列模型训练技术栈。

## Links Into Wiki

- [[recurrent-neural-networks]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
- [[dropout-in-rnns]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
