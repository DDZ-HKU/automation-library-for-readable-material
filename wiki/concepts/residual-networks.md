---
title: Residual Networks
aliases:
  - resnet
  - residual-learning
  - skip-connections
tags:
  - deep-learning
  - computer-vision
  - optimization
  - architecture
updated: 2026-04-16
source_count: 2
status: active
---

# Summary

ResNet 的关键思想不是“网络更深”，而是引入 residual reformulation 和 identity shortcut，让深层网络不必从零逼近目标映射，而可以把很多层理解成对输入表示的渐进修正。这使它同时处在优化问题与架构问题的交界处。

## Current Understanding

- ResNet 要解决的直接问题是 degradation problem：随着深度增加，plain net 的训练误差反而上升。
- 论文把这个问题表述为：如果 identity extension 理论上存在而优化器却找不到，那么困难不在表达能力本身，而在优化路径。
- residual block 通过学习 `F(x)` 并输出 `F(x) + x`，把“学整个函数”改写成“学相对输入的偏移”。
- identity shortcut 的价值在于：它给信息和梯度提供了一条更低阻力的通路，同时几乎不增加参数和计算。
- 这使 ResNet 在初衷上更像一种 optimization-aware reformulation，而不是纯粹追求新型表示关系的架构发明。
- 与 [[highway-networks]] / [highway-networks.md](highway-networks.md) 相比，ResNet 可以看作保留了“跨层直通路径”这一直觉，但把 gated carry path 压缩成更轻量的 identity shortcut。
- 但从后续历史看，skip/residual connections 又变成了深层网络设计中的通用架构基元，因此它后来获得了超出原论文优化叙事的架构地位。
- bottleneck design 表明，当深度继续增长时，残差思路还能和计算效率约束兼容。
- `Identity Mappings in Deep Residual Networks` 进一步说明，shortcut 的价值依赖于尽量保持 identity；在 skip path 上加入 gating、scaling、projection 等 modulation，往往会重新损害信息传播。
- pre-activation residual unit 把 BN/ReLU 前移到权重层之前，等于把 residual branch 清理得更干净，同时让主路径更接近默认直通。
- 因此 residual line 的下一步不是“更复杂的残差控制”，而是“更少干预的 identity path + 更规范的 block 组织”。
- 在当前知识库里，ResNet 是一个很好的判例：它提醒我们有些重大突破并不干净地属于“架构”或“优化”，而是通过重写优化目标来形成新的架构单元。

## Evidence

- 主要依据来自 [[deep-residual-learning-for-image-recognition]] / [../sources/deep-residual-learning-for-image-recognition.md](../sources/deep-residual-learning-for-image-recognition.md)。
- 补充依据来自 [[identity-mappings-in-deep-residual-networks]] / [../sources/identity-mappings-in-deep-residual-networks.md](../sources/identity-mappings-in-deep-residual-networks.md)。
- 与 [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md) 对照看，ResNet 是优化问题被架构化表达的典型案例。
- 与 [[highway-networks]] / [highway-networks.md](highway-networks.md) 对照看，ResNet 不是第一条 skip path 思路，但它把 gating 负担降到了更简单的 identity residual 形式。

## Open Questions

- 在今天视角回看，skip connection 的主要作用应如何分解为优化便利、表示保真与网络组合性提升？
- 如果把 ResNet 放进更广的 agent / LLM 系统设计里，“residual reformulation” 是否对应某类更一般的工程策略，例如把难问题改写成增量修正问题？

## Related Pages

- [[deep-residual-learning-for-image-recognition]] / [../sources/deep-residual-learning-for-image-recognition.md](../sources/deep-residual-learning-for-image-recognition.md)
- [[identity-mappings-in-deep-residual-networks]] / [../sources/identity-mappings-in-deep-residual-networks.md](../sources/identity-mappings-in-deep-residual-networks.md)
- [[highway-networks]] / [highway-networks.md](highway-networks.md)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md)
- [[transformers]] / [transformers.md](transformers.md)
