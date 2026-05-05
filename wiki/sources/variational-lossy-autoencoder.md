---
title: Variational Lossy Autoencoder
source_path: raw/sources/1611.02731v2/1611.02731v2.md
source_type: paper
author: Xi Chen; Diederik P. Kingma; Tim Salimans; Yan Duan; Prafulla Dhariwal; John Schulman; Ilya Sutskever; Pieter Abbeel
published: 2017
processed: 2026-04-16
topics:
  - variational-autoencoders
  - generative-models
  - representation-learning
entities:
  - Xi Chen
  - Diederik P. Kingma
  - Tim Salimans
  - Yan Duan
  - Prafulla Dhariwal
  - John Schulman
  - Ilya Sutskever
  - Pieter Abbeel
status: active
---

# Summary

这篇论文提出 Variational Lossy Autoencoder (VLAE)。它的核心判断是：VAE 的 latent code 不必编码输入中的全部细节，而可以在 decoder 足够强时只保留更高层、全局性的结构信息，把局部纹理或低层统计交给 autoregressive decoder 建模。这样既能得到更有用的 representation，也能提升生成建模效果。

## Core Claims

- 表征学习里，不同任务并不总需要保留输入的全部信息；对图像等数据，global structure 往往比局部纹理更值得进入 latent code。
- 如果把 VAE 与 autoregressive model 结合，并适当设计 encoder / decoder 架构，就可以控制 latent variable 学什么、丢什么。
- 在这种设计下，VAE 会以 lossy 的方式进行“自动编码”：latent code 保留高层信息，而弱相关细节交给 autoregressive decoder。
- autoregressive model 既可用于 prior `p(z)`，也可用于 decoder `p(x|z)`，从而显著增强 VAE 的生成能力。
- VLAE 不只是提升 likelihood，而是把“representation learning”与“powerful generative decoder”之间的关系显式化。
- 论文把这种分工进一步解释为 explicit information placement：通过限制 decoder 的感受野与因子分解方式，来决定哪些信息必须进入 latent code。

## Key Facts

- arXiv 摘要明确将方法表述为结合 VAE 与 RNN、MADE、PixelRNN/CNN 等 autoregressive 模型。
- 论文强调通过架构设计来约束 global latent code 的信息内容，而不是只依赖损失函数口头希望其学到高层特征。
- 第 2 节明确把问题推进到 `bits-back coding` 与 `information preference`：强 decoder 之所以会让 latent 被忽略，并不只是优化问题，也和最优编码分工本身有关。
- 第 3 节提出两块核心结构：
  - 用小感受野 autoregressive decoder 实现 lossy code via explicit information placement
  - 用 autoregressive flow 作为 learnable prior，以提升 bits-back coding 效率
- 第 4 节实验覆盖 Statically/Dynamically Binarized MNIST、OMNIGLOT、Caltech-101 Silhouettes，并给出 competitive 的 CIFAR-10 结果。
- 该工作发表于 ICLR 2017。

## Tensions / Contradictions

- 强 decoder 会不会让 latent variable 退化乃至被忽略，是 VAE 线里的经典张力；这篇论文的回答不是削弱 decoder，而是重新定义 latent code 应该承担的内容。
- 因此它和“避免 posterior collapse”的很多后续工作不完全同类：这里更强调有意让 latent 表征变成有选择的、lossy 的全局编码。
- 这也意味着它既属于 generative modeling，也属于 representation learning，因为它把两者之间的分工关系拿到台面上处理。

## Links Into Wiki

- [[variational-autoencoders]] / [../concepts/variational-autoencoders.md](../concepts/variational-autoencoders.md)
- [[recurrent-neural-networks]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
