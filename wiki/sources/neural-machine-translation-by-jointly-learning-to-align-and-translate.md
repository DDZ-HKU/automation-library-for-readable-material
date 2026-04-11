---
title: Neural Machine Translation by Jointly Learning to Align and Translate
source_path: raw/sources/1409.0473v7/1409.0473v7.md
source_type: paper
author: Dzmitry Bahdanau; Kyunghyun Cho; Yoshua Bengio
published: 2014
processed: 2026-04-09
topics:
  - attention
  - recurrent-neural-networks
  - sequence-to-sequence-models
  - neural-machine-translation
entities:
  - Dzmitry Bahdanau
  - Kyunghyun Cho
  - Yoshua Bengio
status: active
---

# Summary

这篇论文提出了经典的 Bahdanau attention。它的关键不是把 attention 当成新的主架构，而是在 RNN encoder-decoder 内部引入一个可微的 soft alignment 机制，专门缓解“整句必须压成一个 fixed-length vector”这一瓶颈。

## Core Claims

- 传统 RNN encoder-decoder 把整句压成单个 fixed-length context vector，这会成为长句翻译的主要瓶颈。
- 更好的做法不是一次性压缩全部信息，而是在生成每个目标词时，动态从源句注释向量中读取相关部分。
- alignment 应当和翻译模型一起端到端训练，而不是作为单独的潜变量或外部模块事后处理。
- bidirectional encoder 提供的 annotations 比单向最终状态更适合被 decoder 按需读取。
- 这种 attention 机制对长句尤其有效，因为它减少了“必须把所有信息提前塞进单个状态”的压力。

## Key Facts

- 论文提出的模型后来通常被称为 `RNNsearch`，用来对比基础 `RNNencdec`。
- 每个目标位置 `i` 都有自己的 context vector `c_i`，而不是整句共享一个固定上下文。
- `c_i` 由所有源端 annotations 的加权和组成，权重 `alpha_ij` 由 alignment model 计算。
- 这里的 alignment 是 soft alignment，可直接反向传播；作者明确说它不是传统意义上的潜变量。
- 编码端使用 bidirectional RNN，把前向和后向状态拼接成每个源词的 annotation。
- 在英法翻译实验中，作者报告该方法对长句更稳健，效果接近当时最强 phrase-based 系统。

## Tensions / Contradictions

- 这篇论文里的 attention 仍是 RNN seq2seq 的补丁式扩展，而不是后来的 self-attention 主导架构。
- 它缓解的是 fixed-length bottleneck，但没有去掉 decoder 的自回归递归路径，也没有消除顺序计算。
- 论文已经指出需要为每个目标词对所有源词计算权重，这种 `T_x x T_y` 的代价在更长序列或更大任务上会变成限制。
- 从今天回看，这篇论文是从“状态压缩”转向“按需读取”的关键一步，但还没有走到 Transformer 那种统一的 attention-first 设计。

## Links Into Wiki

- [[attention-mechanisms]] / [../concepts/attention-mechanisms.md](../concepts/attention-mechanisms.md)
- [[recurrent-neural-networks]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
- [[transformers]] / [../concepts/transformers.md](../concepts/transformers.md)
- [[attention-is-all-you-need]] / [attention-is-all-you-need.md](attention-is-all-you-need.md)
