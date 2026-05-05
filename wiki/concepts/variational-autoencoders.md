---
title: Variational Autoencoders
aliases:
  - vae
  - variational-inference-generative-models
tags:
  - deep-learning
  - generative-models
  - representation-learning
updated: 2026-04-16
source_count: 1
status: active
---

# Summary

VAE 关心的不只是“从 latent 采样再重建”，而是怎样把生成建模与表征学习绑在一起：latent variable 应该承载哪些统计结构，decoder 又该负责哪些细节。当前知识库中的第一篇材料 `Variational Lossy Autoencoder` 提醒我们，latent code 的价值未必在于保留全部信息，而可能在于只保留更高层、任务更有用的结构。

## Current Understanding

- VAE 可以被看作在显式 latent variable 与可训练 decoder 之间做分工的生成模型。
- 一旦 decoder 足够强，latent code 学什么就不再是“自然发生”的，而是一个需要刻意设计的问题。
- `bits-back coding` 与 `information preference` 提醒我们：如果 decoder 已经能便宜地解释某类统计结构，那么最优编码未必会把这些信息再放进 latent code。
- `Variational Lossy Autoencoder` 给出的判断是：
  - global latent 应优先保留全局结构
  - 局部纹理与低层统计可以交给 autoregressive decoder
  - 因而“lossy autoencoding”不一定是缺陷，也可能是刻意的表征选择
- 这意味着 VAE 的关键问题之一不是“怎样让 latent 保留更多信息”，而是“哪些信息值得由 latent 保留，哪些信息应交给 decoder 局部建模”。
- 在这条理解下，autoregressive decoder 不是 latent 的敌人，而是表征分工中的另一半：它越擅长局部统计，latent 就越可以专注于更稀缺的全局因素。
- autoregressive flow prior 的价值也不只是更强 prior，而是提高 bits-back coding 效率，使“有用 latent”与“高 likelihood”之间的冲突减弱。
- 这让 VAE 主题不只是概率建模问题，也变成 representation learning 中“该压缩什么、不该压缩什么”的结构问题。

## Evidence

- 当前主要依据来自 [[variational-lossy-autoencoder]] / [../sources/variational-lossy-autoencoder.md](../sources/variational-lossy-autoencoder.md)。

## What This Changes

- 它修正了一个常见直觉：`latent 没被用上 = 模型失败`。更准确的判断是：latent 是否承担了那些 decoder 不应承担、但下游任务更在意的结构信息。
- 它也把 VAE 讨论从单纯的 ELBO 优化技巧，推进到信息分配与结构偏置设计。

## Open Questions

- 强 autoregressive decoder 与 latent usefulness 之间的张力，后来是如何被系统化处理的？
- “lossy latent for global structure” 与后续 disentanglement / hierarchical VAE 线路是什么关系？
- 在今天回看，VAE 的关键难点更像 inference、objective design，还是 representation allocation？

## Related Pages

- [[variational-lossy-autoencoder]] / [../sources/variational-lossy-autoencoder.md](../sources/variational-lossy-autoencoder.md)
- [[how-to-think-about-decoder-strength-and-latent-usefulness-in-vaes]] / [../notes/cases/how-to-think-about-decoder-strength-and-latent-usefulness-in-vaes.md](../notes/cases/how-to-think-about-decoder-strength-and-latent-usefulness-in-vaes.md)
- [[recurrent-neural-networks]] / [recurrent-neural-networks.md](recurrent-neural-networks.md)
