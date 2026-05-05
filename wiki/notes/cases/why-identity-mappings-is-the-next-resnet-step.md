---
title: Why Identity Mappings Is the Next ResNet Step
updated: 2026-04-16
status: active
---

# Summary

这页原本记录“为什么 `Identity Mappings in Deep Residual Networks` 应该是视觉分支的下一篇”。现在该论文已入库，结论得到验证：它确实不是重复 ResNet，而是把 residual line 从“有效技巧”推进成“更干净的 identity / pre-activation 结构原则”。

## Confirmed Understanding

- [[highway-networks]] / [../../concepts/highway-networks.md](../../concepts/highway-networks.md) 已确认，Highway Networks 解决的是 gated carry/transform path 如何让极深网络更可训练。
- [[residual-networks]] / [../../concepts/residual-networks.md](../../concepts/residual-networks.md) 已确认，ResNet 把 skip path 思想压缩成更轻量的 identity shortcut + residual reformulation。
- [[highway-networks-to-resnet-transition]] / [highway-networks-to-resnet-transition.md](highway-networks-to-resnet-transition.md) 已确认，Highway 与 ResNet 的差别可压缩为“受控信息流” vs “默认直通 + 增量修正”。
- [[identity-mappings-in-deep-residual-networks]] / [../../sources/identity-mappings-in-deep-residual-networks.md](../../sources/identity-mappings-in-deep-residual-networks.md) 已确认，residual line 的下一步不是继续给 shortcut 加控制，而是尽量保持 identity path 干净，并用 pre-activation 重组 residual unit。

## Tacit Interpretation

- 这条 residual line 现在已经从“桥梁”延长成了三段演化：
  - Highway：受控信息流
  - ResNet：默认直通 + 增量修正
  - Identity Mappings：进一步清理主路径，减少对直通路径的干预
- 这说明 residual line 的成熟方向不是更复杂的 gate，而是更干净的 shortcut、更少干预的主路径，以及更规范的 block 组织。

## What This Teaches

- 一条技术线真正可迁移的部分，常常不在首个爆发点，而在后续那一步“怎样把有效技巧清理成稳定默认结构”。
- `Identity Mappings...` 证明，很多 follow-up 论文的价值不在加新机制，而在删掉妨碍主路径传播的东西。

## How To Apply

- 现在可以把当前视觉分支的 residual 线理解成：
  - `Highway -> ResNet -> Identity/Pre-activation`
- 后续再补视觉论文时，可以优先找“某条线怎样从 breakthrough 进入 default pattern”的材料，而不是只补新的 headline 模型。

## Remaining Questions

- pre-activation 这一步后来是如何进一步影响 ResNet family 的默认 recipe，例如 BN/initialization/block ordering 的整体配套？
- 在更广的系统设计里，`keep the main path clean` 能否作为比“残差”更一般的迁移原则？

## Links

- [[highway-networks]] / [../../concepts/highway-networks.md](../../concepts/highway-networks.md)
- [[residual-networks]] / [../../concepts/residual-networks.md](../../concepts/residual-networks.md)
- [[highway-networks-to-resnet-transition]] / [highway-networks-to-resnet-transition.md](highway-networks-to-resnet-transition.md)
- [[identity-mappings-in-deep-residual-networks]] / [../../sources/identity-mappings-in-deep-residual-networks.md](../../sources/identity-mappings-in-deep-residual-networks.md)
