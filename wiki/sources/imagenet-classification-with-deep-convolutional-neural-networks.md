---
title: ImageNet Classification with Deep Convolutional Neural Networks
source_path: raw/sources/NIPS-2012-imagenet-classification-with-deep-convolutional-neural-networks-Paper/NIPS-2012-imagenet-classification-with-deep-convolutional-neural-networks-Paper.md
source_type: paper
author: Alex Krizhevsky; Ilya Sutskever; Geoffrey E. Hinton
published: 2012
processed: 2026-04-11
topics:
  - alexnet
  - computer-vision
  - convolutional-neural-networks
  - scaling
entities:
  - Alex Krizhevsky
  - Ilya Sutskever
  - Geoffrey E. Hinton
status: active
---

# Summary

这篇论文提出了通常被称为 AlexNet 的模型。它的重要性不只是“一个更深的 CNN”，而是第一次把大规模 ImageNet 数据、深卷积网络、GPU 训练、ReLU 激活和 dropout 正则化成功组合成一个能在真实大规模视觉基准上显著超越既有方法的系统方案。

## Core Claims

- 大规模视觉识别要真正突破，不能只靠更好的手工特征，还需要高容量模型与足够大的数据集同时成立。
- 深卷积网络一旦结合可行的 GPU 训练实现，就能在 ImageNet 规模上显著超越传统视觉流水线。
- non-saturating ReLU 比传统饱和激活训练得更快，是大模型可训练性的关键因素。
- dropout 对大规模全连接层的过拟合控制很有效。
- GPU 计算不只是加速细节，而是让这类模型规模首次现实可用的系统前提。

## Key Facts

- 论文报告在 ImageNet LSVRC-2010 上达到 37.5% top-1 和 17.0% top-5 error。
- ILSVRC-2012 提交版本达到 15.3% top-5 test error，远优于第二名 26.2%。
- 模型包含 5 个卷积层和 3 个全连接层，约 6000 万参数。
- 作者使用双 GPU 训练来突破单卡显存约束。
- 论文明确把 ReLU、dropout、data augmentation 和高效 GPU 卷积实现都列为结果成立的重要组成部分。

## Tensions / Contradictions

- AlexNet 的影响横跨三层：它既是架构工作，也是优化/正则化工作，还是系统实现工作。
- 从今天视角回看，它最重要的并不是单个部件都新，而是它首次证明“深度视觉 + 大规模训练 + 工程实现”能够共同成立。
- 因此它更像一次 scaling breakthrough，而不只是单篇架构论文。

## Links Into Wiki

- [[alexnet]] / [../concepts/alexnet.md](../concepts/alexnet.md)
- [[highway-networks]] / [../concepts/highway-networks.md](../concepts/highway-networks.md)
- [[residual-networks]] / [../concepts/residual-networks.md](../concepts/residual-networks.md)
