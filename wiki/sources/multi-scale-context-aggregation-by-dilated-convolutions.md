---
title: Multi-Scale Context Aggregation by Dilated Convolutions
source_path: raw/sources/1511.07122v3/1511.07122v3.md
source_type: paper
author: Fisher Yu; Vladlen Koltun
published: 2015
processed: 2026-04-11
topics:
  - dilated-convolutions
  - semantic-segmentation
  - computer-vision
  - dense-prediction
entities:
  - Fisher Yu
  - Vladlen Koltun
status: active
---

# Summary

这篇论文提出用 dilated convolutions 做 multi-scale context aggregation。它的核心贡献不是单纯改进分类网络，而是明确指出 dense prediction 与 image classification 的结构目标不同，因此需要一种在不降低分辨率的前提下扩张感受野的专用模块。

## Core Claims

- semantic segmentation 这类 dense prediction 问题，不应只被视为 classification network 的下游适配。
- 对 dense prediction 来说，关键矛盾是：既要大感受野做 multi-scale reasoning，又要保留 full-resolution output。
- dilated convolution 可以在不丢失分辨率和 coverage 的前提下指数式扩大 receptive field。
- 因此，应当设计 dedicated context module，而不是默认沿用 classification-style pooling/downsampling 结构。
- 某些从分类网络继承来的组件在 dense prediction 场景里其实是 vestigial components，去掉后反而更准。

## Key Facts

- 论文给出 dilated convolution 的形式化定义，并强调它不是“构造一个被拉伸的卷积核”，而是改变卷积操作本身。
- 作者展示了按 `1, 2, 4, ...` 扩张率叠加时，receptive field 可以指数增长，而参数量只线性增长。
- 论文提出 context module：一个没有 pooling/subsampling 的矩形卷积模块，专门为 dense prediction 聚合上下文。
- 在 Pascal VOC 2012 上，将 context module 插到既有 segmentation front end 后，可稳定提升精度。
- 作者同时指出，适配 dense prediction 时，分类网络里某些遗留设计会损害性能。

## Tensions / Contradictions

- 这篇工作与 ResNet/Highway Networks 不同，它关心的不是“更深网络怎么训”，而是“dense prediction 到底需要什么样的上下文结构”。
- 它仍然使用 convolutional inductive bias，但重新分配了 receptive field expansion 与 resolution preservation 之间的取舍。
- 从问题分层看，这篇更偏 architecture for task structure，而不是纯优化或系统扩展。

## Links Into Wiki

- [[dilated-convolutions]] / [../concepts/dilated-convolutions.md](../concepts/dilated-convolutions.md)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md)
