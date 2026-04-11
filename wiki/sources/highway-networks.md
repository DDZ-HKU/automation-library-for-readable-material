---
title: Highway Networks
source_path: raw/sources/1505.00387v2/1505.00387v2.md
source_type: paper
author: Rupesh Kumar Srivastava; Klaus Greff; Jurgen Schmidhuber
published: 2015
processed: 2026-04-10
topics:
  - highway-networks
  - optimization
  - deep-learning
  - computer-vision
entities:
  - Rupesh Kumar Srivastava
  - Klaus Greff
  - Jurgen Schmidhuber
status: active
---

# Summary

这篇论文提出 Highway Networks。它的核心思想是给深层前馈网络加入可学习的 transform/carry gating，使信息能够沿“information highways”跨层传递，从而显著缓解极深网络的优化困难。

## Core Claims

- 随着深度增加，plain deep nets 的优化会迅速恶化，单靠更好的初始化并不足以支撑极深网络训练。
- 通过引入受 LSTM 启发的 gating mechanism，前馈网络也可以学会在多层之间调节“变换多少”和“直接携带多少”信息。
- Highway layer 可以在 plain transform 与近似 identity pass-through 之间平滑切换。
- 对 transform gate 使用负偏置初始化，使网络初始更偏向 carry behavior，可以显著改善极深网络的可训练性。
- Highway networks 可以用普通 SGD 直接训练到数百层，而不必依赖逐层预训练或 teacher-student 程序。

## Key Facts

- 论文把 layer 写成 `H(x) * T(x) + x * (1 - T(x))`，其中 `T` 是 transform gate。
- gating 设计明确受 LSTM forget/transfer 直觉启发。
- 作者报告 highway nets 深到 100 甚至 900 层时仍可优化。
- 在 CIFAR-10 上，作者展示了可直接训练到与 FitNets 相近的效果，而无需教师网络。
- 文中还可视化了 transform gate 与 block output，说明网络确实在大量使用 carry paths，而不是只把 gating 当装饰。

## Tensions / Contradictions

- 这篇工作更像 optimization-oriented architecture：它通过一个新的结构单元解决优化问题，但核心卖点仍是“可训练性”，不是新的表示关系。
- 与后来的 ResNet 相比，Highway Networks 需要数据依赖的 gate 和额外参数，因此表达更灵活，但也更重。
- 从今天回看，Highway Networks 是 skip-connection 时代的关键过渡物：它已经抓住了“跨层直通路径”这件事，但还没有走到 ResNet 那种 parameter-free identity shortcut 的极简形式。

## Links Into Wiki

- [[highway-networks]] / [../concepts/highway-networks.md](../concepts/highway-networks.md)
- [[residual-networks]] / [../concepts/residual-networks.md](../concepts/residual-networks.md)
- [[recurrent-neural-networks]] / [../concepts/recurrent-neural-networks.md](../concepts/recurrent-neural-networks.md)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md)
