---
title: The Unreasonable Effectiveness of Recurrent Neural Networks
source_path: raw/The Unreasonable Effectiveness of Recurrent Neural Networks.md
source_type: blog-post
author: Andrej Karpathy
published: 2015-05-21
processed: 2026-04-08
topics:
  - recurrent-neural-networks
  - lstm
  - character-level-language-models
  - generative-models
entities:
  - Andrej Karpathy
status: active
---

# Summary

Andrej Karpathy 这篇文章用通俗但技术上扎实的方式解释了 RNN/LSTM 如何处理序列、如何训练字符级语言模型，以及为什么这类模型即使在字符层面也能学到强烈的语法、格式和风格结构。

## Core Claims

- RNN 的关键优势是能够处理任意长度的序列输入、输出或两者同时存在的任务。
- 从程序视角看，RNN 可以被理解为带内部状态的可学习程序，因此比固定步数的前馈网络更适合序列建模。
- 在实践中，LSTM 往往比 vanilla RNN 更好用，因为其更新机制和反向传播动态更稳定。
- 字符级语言模型即使只看字符，也能学到相当丰富的语言、格式和结构模式。
- 模型不仅能学习自然语言风格，还能学习结构化文本格式，如 Markdown、XML、LaTeX 和代码的局部语法。

## Key Facts

- 文章配套发布了 `char-rnn` 代码，用于训练基于多层 LSTM 的字符级语言模型。
- 文章解释了 RNN 的典型任务范式：固定输入到固定输出、固定输入到序列输出、序列输入到固定输出、序列到序列、同步序列标注。
- 训练字符级语言模型时，模型学习在给定前文字符的情况下预测下一个字符的概率分布。
- 采样阶段可通过 temperature 控制输出的保守性与多样性。
- 文中展示了在 Paul Graham 文集、莎士比亚、Wikipedia、LaTeX 数学文本和 Linux 源代码上的生成样本。
- 文章强调，模型常能学会局部和中程结构，但在长程依赖上仍会出错，例如 LaTeX 环境闭合错误、代码变量一致性问题等。

## Tensions / Contradictions

- 生成结果常表现出强语法拟合能力，但并不等于语义理解或事实正确。
- 样本在局部形式上可能非常像真文本，但会出现幻觉内容、错误链接、伪造 ID 和不一致变量名。
- 文章展示了 RNN 的“惊人效果”，但从今天视角看，其讨论主要代表 pre-Transformer 时代的序列建模范式。

## Links Into Wiki

- [[recurrent-neural-networks]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
- [[character-level-language-models]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
