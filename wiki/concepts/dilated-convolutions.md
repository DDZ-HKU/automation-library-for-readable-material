---
title: Dilated Convolutions
aliases:
  - atrous-convolutions
  - context-aggregation
tags:
  - deep-learning
  - computer-vision
  - dense-prediction
  - architecture
updated: 2026-04-11
source_count: 1
status: active
---

# Summary

Dilated convolution 的核心价值，是在不做 pooling/downsampling 的情况下扩大 receptive field。它因此特别适合 dense prediction：既保留分辨率，又能聚合更大范围的上下文。

## Current Understanding

- dense prediction 与 image classification 的结构目标不同，不能默认复用 classification backbone 的全部设计。
- 对 segmentation 来说，关键困难不是只看更大上下文，而是在不丢失空间精度的同时看更大上下文。
- dilated convolution 通过改变卷积采样间隔来扩大感受野，而不改变 feature map resolution。
- 因此它代表一种明确的 architecture judgment：不要总用更深、更池化、更下采样来换上下文，也可以用更稀疏的卷积支持 multi-scale reasoning。
- 这篇工作的重要性还在于，它直接把“dense prediction 需要什么结构”作为一等问题提出，而不是继续把分类网络当默认母体。
- 在当前知识库里，它可以被视作“任务结构驱动架构设计”的案例，而不是“纯粹更强 backbone”的案例。

## Evidence

- 主要依据来自 [[multi-scale-context-aggregation-by-dilated-convolutions]] / [../sources/multi-scale-context-aggregation-by-dilated-convolutions.md](../sources/multi-scale-context-aggregation-by-dilated-convolutions.md)。
- 与 [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md) 对照看，它是“按任务结构改架构”的典型架构问题。

## Open Questions

- 从今天视角回看，dilated convolutions 的长期价值更多体现在感受野控制、dense prediction 任务适配，还是作为 later segmentation systems 的标准模块？
- 在更现代的视觉架构里，dilated convolution 与 attention-based context aggregation 的边界应如何理解？

## Related Pages

- [[multi-scale-context-aggregation-by-dilated-convolutions]] / [../sources/multi-scale-context-aggregation-by-dilated-convolutions.md](../sources/multi-scale-context-aggregation-by-dilated-convolutions.md)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md)
