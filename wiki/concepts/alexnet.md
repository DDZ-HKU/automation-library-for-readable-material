---
title: AlexNet
aliases:
  - imagenet-cnn-breakthrough
  - deep-convolutional-neural-networks-for-imagenet
tags:
  - deep-learning
  - computer-vision
  - scaling
  - architecture
updated: 2026-04-11
source_count: 1
status: active
---

# Summary

AlexNet 的真正意义，不在某个单独组件，而在于它把大数据集、较深 CNN、GPU 训练、ReLU 和 dropout 统一成一个第一次在 ImageNet 规模上压倒性成立的方案。它是视觉深度学习主线的规模化起点。

## Current Understanding

- AlexNet 标志着视觉深度学习从“小规模上可行”走向“大规模上决定性有效”。
- 它回答的核心问题不是“更深网络如何可训练”，而是“深度视觉模型何时真正跨过规模门槛”。
- 这篇工作的影响不能被简单归类成架构、优化或系统中的某一类，因为它的突破来自三者同时就位。
- 在当前视觉材料里，AlexNet 应被放在 Highway/ResNet 和 dense prediction 分支之前，作为更早的共同母线。
- 如果说 Highway/ResNet 继续处理的是“更深网络怎么训”，那么 AlexNet 更早处理的是“为什么深度视觉终于值得认真做大”。

## Evidence

- 主要依据来自 [[imagenet-classification-with-deep-convolutional-neural-networks]] / [../sources/imagenet-classification-with-deep-convolutional-neural-networks.md](../sources/imagenet-classification-with-deep-convolutional-neural-networks.md)。

## Open Questions

- AlexNet 的长期可迁移资产，到底是 CNN 结构本身，还是一种“数据 + 算力 + 训练技巧”必须一起放大的工程方法？
- 从今天回看，AlexNet 的历史地位中，GPU 实现与 ReLU/dropout 的权重各有多大？

## Related Pages

- [[imagenet-classification-with-deep-convolutional-neural-networks]] / [../sources/imagenet-classification-with-deep-convolutional-neural-networks.md](../sources/imagenet-classification-with-deep-convolutional-neural-networks.md)
- [[highway-networks]] / [highway-networks.md](highway-networks.md)
- [[residual-networks]] / [residual-networks.md](residual-networks.md)
- [[dilated-convolutions]] / [dilated-convolutions.md](dilated-convolutions.md)
