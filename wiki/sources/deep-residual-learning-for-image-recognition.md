---
title: Deep Residual Learning for Image Recognition
source_path: raw/sources/1512.03385v1/1512.03385v1.md
source_type: paper
author: Kaiming He; Xiangyu Zhang; Shaoqing Ren; Jian Sun
published: 2015
processed: 2026-04-10
topics:
  - residual-networks
  - computer-vision
  - convolutional-neural-networks
  - optimization
entities:
  - Kaiming He
  - Xiangyu Zhang
  - Shaoqing Ren
  - Jian Sun
status: active
---

# Summary

这篇论文提出了 ResNet。它的核心贡献不只是“把卷积网络堆得更深”，而是把深层网络训练困难重写成一个 residual reformulation 问题：与其直接学习目标映射，不如学习相对输入的残差，并通过 identity shortcut 保留一条低阻力信息路径。

## Core Claims

- 深层网络并不是单纯因为过拟合才变差，更关键的问题是存在 optimization degradation：层数加深后训练误差反而上升。
- 如果更深模型理论上至少能复制浅层模型的 identity extension，但优化器实际找不到这种解，就说明问题出在优化路径，而不只是容量或泛化。
- 让堆叠层去学习 residual mapping `F(x) = H(x) - x`，往往比直接学习 `H(x)` 更容易优化。
- parameter-free identity shortcuts 可以在几乎不增加计算和参数的前提下显著缓解 degradation problem。
- 更深的 residual nets 不仅更容易优化，而且确实可以从更大深度中获得更高精度。

## Key Facts

- 论文在 ImageNet 上评估了最高 152 层的 residual net，并报告其复杂度仍低于 VGG。
- 该方法在 ILSVRC 2015 classification 上取得 3.57% top-5 ensemble error，并夺冠。
- 论文把 plain 18/34-layer nets 与对应 ResNet 直接对比，显示 deeper plain net 训练误差更高，而 deeper ResNet 则相反。
- 对 shortcut 的比较里，作者指出 projection shortcut 并非解决 degradation 的必要条件，identity shortcut 已能解决主要问题。
- 对更深网络，论文采用 bottleneck block，把 `1x1 -> 3x3 -> 1x1` 作为更经济的 residual unit。
- 在 CIFAR-10 上，作者进一步展示了 100 和 1000 层级别 residual nets 的可训练性。

## Tensions / Contradictions

- 这篇论文的叙述同时跨了两层：它既像一个 optimization reformulation，也带来了可迁移的 architectural primitive。
- 论文强调的是“更容易优化”，而不是残差连接本身直接增加表示能力；但从后续历史看，shortcut 又确实变成了架构设计的核心基元。
- 因此 ResNet 不宜被简单归类成“纯架构创新”或“纯优化技巧”，更准确的说法是：它把优化困难重写成一种可架构化的解决方案。

## Links Into Wiki

- [[residual-networks]] / [../concepts/residual-networks.md](../concepts/residual-networks.md)
- [[transformers]] / [../concepts/transformers.md](../concepts/transformers.md)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md)
