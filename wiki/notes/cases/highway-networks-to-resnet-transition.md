---
title: Highway Networks to ResNet Transition
updated: 2026-04-10
status: active
---

# Summary

Highway Networks 到 ResNet 这条线真正教会人的，不只是“skip connection 有用”，而是：同样在解决深层网络优化困难时，系统可以选择“更强的控制”或“更强的默认直通”。Highway 选择了前者，ResNet 选择了后者，而后者后来被证明更轻、更稳、也更容易成为通用基元。

## Confirmed Understanding

- [[highway-networks]] / [../../concepts/highway-networks.md](../../concepts/highway-networks.md) 已确认，Highway Networks 通过 gated carry/transform path 来缓解 extremely deep nets 的优化困难。
- 该页还确认，Highway 明显受 LSTM gating 直觉影响，把“信息是否通过”交给可学习 gate 决定。
- [[residual-networks]] / [../../concepts/residual-networks.md](../../concepts/residual-networks.md) 已确认，ResNet 通过 residual reformulation 与 identity shortcut 缓解 degradation problem。
- 同一页还确认，ResNet 可以被看作保留了 skip path 思想，但把 gated carry 压缩成更轻量 identity shortcut 的形式。

## Tacit Interpretation

- Highway 和 ResNet 不是两条互不相关的线，而是同一个问题的两种回答。
- Highway 的回答是：
  - 深层网络难训
  - 所以要增加更细的控制
  - 让 gate 决定该保留多少旧信息
- ResNet 的回答是：
  - 深层网络难训
  - 所以先假设旧信息默认应该能过
  - 新层只需要学习对旧表示的增量修正
- 这背后其实是两种工程哲学：
  - `controlled flow`
  - `default pass-through + delta update`
- 后来更成功的往往是第二种，不是因为它更“聪明”，而是因为它把默认行为设得更稳，把复杂性压得更低。

## What This Teaches

- 面对优化困难时，不要默认解决方案一定是“加更多控制器”。
- 有时更强的做法是把系统重写成：
  - 默认有一条稳定主路径
  - 额外模块只负责小幅修正
- 这类思路不仅适用于网络结构，也适用于很多工程系统：
  - 默认安全路径
  - 局部增量修改
  - 而不是处处门控、处处决策

## How To Think

遇到两个都声称“改善可训练性”的方法时，可以问：

1. 它是通过增加控制自由度解决问题，还是通过减少必须学习的负担解决问题？
2. 它的默认路径是“什么都要学”，还是“先允许通过，再做修正”？
3. 它增加的是更多参数化控制，还是更强的结构先验？
4. 哪种设计更可能成为长期通用基元？

## How To Apply

- 读后续模型论文时，可以用 Highway vs ResNet 这组对照来判断：
  - 一个新模块是在“加控制器”
  - 还是在“加稳定主路径”
- 做系统设计时，也可以迁移这个判断：
  - 如果某条主链本来就应该大部分保持不变，就让它默认直通
  - 把学习或推理成本集中在增量修正上

## To Be Verified

- 当前这条解读主要建立在 Highway Networks 扩展摘要和 ResNet 原始论文上，尚未纳入更完整的 1507.06228 长文与 ResNet 后续 pre-activation 论文。
- 对“为什么社区最后更偏向 ResNet”的解释，目前仍偏结构简洁性与优化稳定性的推断。

## Links

- [[highway-networks]] / [../../concepts/highway-networks.md](../../concepts/highway-networks.md)
- [[residual-networks]] / [../../concepts/residual-networks.md](../../concepts/residual-networks.md)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md)
