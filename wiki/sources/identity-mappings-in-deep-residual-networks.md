---
title: Identity Mappings in Deep Residual Networks
source_path: raw/sources/1603.05027v3/1603.05027v3.md
source_type: paper
author: Kaiming He; Xiangyu Zhang; Shaoqing Ren; Jian Sun
published: 2016
processed: 2026-04-16
topics:
  - residual-networks
  - optimization
  - deep-learning
  - computer-vision
entities:
  - Kaiming He
  - Xiangyu Zhang
  - Shaoqing Ren
  - Jian Sun
status: active
---

# Summary

这篇论文把 ResNet 从“有效的 residual reformulation”继续推进成更稳定的结构原则。它的核心判断是：如果 shortcut 和 after-addition path 尽量保持 identity，信息与梯度就能更直接地跨层传播；而一旦在 shortcut 上加入 gating、projection 或其他 modulation，优化会重新变难。基于这个分析，作者提出 pre-activation residual unit，把 BN 和 ReLU 前移到权重层之前。

## Core Claims

- ResNet 的优势不仅来自 residual form 本身，还来自 skip path 与信号路径尽量接近 identity 这一结构条件。
- 如果 skip connection 和加法后的映射都是 identity，前向与反向信号都可以跨 block 直接传播，这会显著缓解极深网络的优化困难。
- 对 shortcut 做 scaling、gating、`1x1` convolution 或 dropout 等 modulation，通常会破坏这种直接传播路径，使训练更困难。
- 将 BN 和 ReLU 放到卷积之前形成 pre-activation residual unit，可以让残差分支更干净，同时让 shortcut 更接近真正的 identity path。
- pre-activation 设计不仅更容易优化，也表现出更好的正则化效果。

## Key Facts

- 论文明确把原始 ResNet 的问题推进到 “how to keep the path clean” 的层次，而不只是重复证明 residual learning 有效。
- 作者比较了 identity shortcuts 与多种被调制的 shortcuts，结论是后者会削弱信息直通优势。
- 在 CIFAR-10 的 shortcut 对照里，constant scaling、dropout shortcut 与多数 gating / `1x1` shortcut 变体都比 identity shortcut 更难优化，部分设置甚至直接失败。
- 提出的 pre-activation unit 把 activation 从 addition 之后移到每个 weight layer 之前。
- activation 对照里，full pre-activation 在 ResNet-110 与 ResNet-164 上都优于原始 post-activation unit。
- 论文报告 1001-layer pre-activation ResNet 在 CIFAR-10 上达到 4.62% error。
- 在 ImageNet 上，200-layer pre-activation ResNet 的结果优于原始 152-layer ResNet。

## Tensions / Contradictions

- 原始 ResNet 已经把 shortcut 作为关键基元引入，但这篇论文进一步表明：shortcut 不是“有就行”，它的价值依赖于尽量少干预的 identity 形式。
- 因此 residual line 的后续推进不是继续增加控制，而是继续清理主路径，把 block 组织得更接近默认直通。
- 这也强化了一个更一般的判断：很多成功结构的后续优化，不是加更多机制，而是去掉妨碍主路径传播的部件。

## Links Into Wiki

- [[residual-networks]] / [../concepts/residual-networks.md](../concepts/residual-networks.md)
- [[deep-residual-learning-for-image-recognition]] / [deep-residual-learning-for-image-recognition.md](deep-residual-learning-for-image-recognition.md)
- [[highway-networks]] / [highway-networks.md](highway-networks.md)
- [[highway-networks-to-resnet-transition]] / [../notes/cases/highway-networks-to-resnet-transition.md](../notes/cases/highway-networks-to-resnet-transition.md)
- [[why-identity-mappings-is-the-next-resnet-step]] / [../notes/cases/why-identity-mappings-is-the-next-resnet-step.md](../notes/cases/why-identity-mappings-is-the-next-resnet-step.md)
