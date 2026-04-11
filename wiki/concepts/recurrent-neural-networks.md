---
title: Recurrent Neural Networks
aliases:
  - rnn
  - lstm
  - character-level-language-models
tags:
  - deep-learning
  - sequence-modeling
  - language-models
updated: 2026-04-09
source_count: 6
status: active
---

# Summary

RNN 是一类通过隐藏状态递归处理序列的神经网络，而 LSTM 是其中最关键的工程变体之一；在当前知识库里，这条主题线关注的是它们为什么适合序列建模、LSTM 如何缓解长程依赖问题，以及这类模型的能力边界。

## Current Understanding

- RNN 通过重复应用同一个状态更新函数来处理序列，因此天然支持可变长度输入和输出。
- 与固定深度前馈网络相比，RNN 更像是在优化一个带状态的程序。
- vanilla RNN 提供了最基础的递归更新形式，而 LSTM 通过更复杂的门控机制改善了训练稳定性和记忆能力。
- LSTM 的核心是 cell state，它提供了一条更容易跨时间步传递信息的通道。
- forget gate、input gate 和 output gate 共同控制保留、写入和暴露哪些状态信息。
- 字符级语言模型是理解 RNN 能力的直观切口，因为它要求模型只从字符统计中恢复拼写、语法、格式和部分风格规律。
- 这类模型能学到很多结构规律，但对长程一致性、事实正确性和全局语义的掌握有限。
- LSTM 训练中的一个关键工程问题是正则化：naive dropout 会伤害循环记忆，而只对非循环连接加 dropout 往往更有效。
- 从历史脉络看，LSTM 是标准 RNN 走向实用的重要一步，而 attention 被不少研究者视为下一次关键跃迁。
- Bahdanau attention 说明，RNN/seq2seq 的核心瓶颈之一不只是梯度传播，而是 encoder-decoder 需要把整句压进一个 fixed-length context vector。
- 这一步的重要性在于：attention 最初并不是完全替代 RNN，而是先作为 RNN 的可微检索补丁，缓解状态压缩和长句翻译退化问题。
- 在 seq2seq 范式下，很多任务即使对象本质更像 set，仍会被强行线性化；这时输入或输出顺序的选择会显著影响训练效果。
- 这说明 pre-Transformer 时代不少“结构建模能力”其实部分依赖于人为选择的序列化方式，而不只是模型本身自动学会了结构。
- Transformer 后来的突破，可以理解为把 attention 从 RNN 外围的辅助机制，推进成主要的信息访问与表示计算机制。

## Evidence

- 主要依据来自 [[the-unreasonable-effectiveness-of-recurrent-neural-networks]] / [../sources/the-unreasonable-effectiveness-of-recurrent-neural-networks.md](../sources/the-unreasonable-effectiveness-of-recurrent-neural-networks.md)。
- 关于 LSTM 内部机制和长程依赖问题的解释，主要补充来自 [[understanding-lstm-networks]] / [../sources/understanding-lstm-networks.md](../sources/understanding-lstm-networks.md)。
- 关于 LSTM dropout 正则化的工程经验，补充来自 [[recurrent-neural-network-regularization]] / [../sources/recurrent-neural-network-regularization.md](../sources/recurrent-neural-network-regularization.md)。
- 关于 seq2seq 在集合输入/输出上的扩展，以及顺序选择为何影响性能，补充来自 [[order-matters-sequence-to-sequence-for-sets]] / [../sources/order-matters-sequence-to-sequence-for-sets.md](../sources/order-matters-sequence-to-sequence-for-sets.md)。
- 关于 attention 如何先作为 RNN encoder-decoder 的对齐与检索机制出现，补充来自 [[neural-machine-translation-by-jointly-learning-to-align-and-translate]] / [../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md](../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md)。
- 关于 Transformer 如何去掉 recurrent path、转向 self-attention 主导的架构，补充来自 [[the-annotated-transformer]] / [../sources/the-annotated-transformer.md](../sources/the-annotated-transformer.md)。
- 文中跨多类数据展示了能力边界：自然语言、Wikipedia 标记、LaTeX、Linux C 代码。

## Open Questions

- 这些样本展示的“结构拟合能力”与“真正的抽象理解”边界在哪里？
- 从今天视角回看，RNN/LSTM 相比 Transformer 的主要能力差异应如何总结？
- 哪些现象属于序列建模本身，哪些现象只是大规模数据上的统计拟合？
- LSTM 的门控设计在多大程度上真正缓解了梯度问题，又在多大程度上只是工程上更可训练？
- 对 RNN/LSTM 来说，最稳健的正则化方案边界到底在哪里？哪些经验法则能跨任务迁移？
- 当任务对象并不天然有顺序时，seq2seq 的性能究竟有多少取决于“选对线性化方式”？
- attention 从“辅助读取 set 的机制”演化成“主要建模范式”的关键断点在哪里？
- RNN + attention 与纯 attention 架构的真正边界，应放在“是否保留 recurrent state 作为主路径”还是放在别的结构差异上？

## Related Pages

- [[the-unreasonable-effectiveness-of-recurrent-neural-networks]] / [../sources/the-unreasonable-effectiveness-of-recurrent-neural-networks.md](../sources/the-unreasonable-effectiveness-of-recurrent-neural-networks.md)
- [[understanding-lstm-networks]] / [../sources/understanding-lstm-networks.md](../sources/understanding-lstm-networks.md)
- [[recurrent-neural-network-regularization]] / [../sources/recurrent-neural-network-regularization.md](../sources/recurrent-neural-network-regularization.md)
- [[order-matters-sequence-to-sequence-for-sets]] / [../sources/order-matters-sequence-to-sequence-for-sets.md](../sources/order-matters-sequence-to-sequence-for-sets.md)
- [[neural-machine-translation-by-jointly-learning-to-align-and-translate]] / [../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md](../sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md)
- [[attention-mechanisms]] / [attention-mechanisms.md](attention-mechanisms.md)
- [[sequence-to-sequence-for-sets]] / [sequence-to-sequence-for-sets.md](sequence-to-sequence-for-sets.md)
- [[transformers]] / [transformers.md](transformers.md)
- [[complextropy]] / [complextropy.md](complextropy.md)
