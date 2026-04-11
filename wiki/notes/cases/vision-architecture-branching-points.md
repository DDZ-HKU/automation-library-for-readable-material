---
title: Vision Architecture Branching Points
updated: 2026-04-11
status: active
---

# Summary

当前视觉侧材料已经显示，视觉架构演化并不是一条单线，而至少分成了三条不同问题线：一条围绕“视觉深度学习何时在规模上变得现实”，一条围绕“深层网络如何可训练”，另一条围绕“dense prediction 需要什么结构”。`AlexNet` 属于第一条，`Highway Networks -> ResNet` 属于第二条，`Dilated Convolutions` 属于第三条。

## Confirmed Understanding

- [[alexnet]] / [../../concepts/alexnet.md](../../concepts/alexnet.md) 已确认，其核心价值是把大数据、GPU、ReLU 和 dropout 统一成视觉深度学习的规模化突破。
- [[highway-networks]] / [../../concepts/highway-networks.md](../../concepts/highway-networks.md) 已确认，其核心问题是极深网络的优化与信息流。
- [[residual-networks]] / [../../concepts/residual-networks.md](../../concepts/residual-networks.md) 已确认，其核心优势是把优化困难改写成更轻量的 residual reformulation。
- [[dilated-convolutions]] / [../../concepts/dilated-convolutions.md](../../concepts/dilated-convolutions.md) 已确认，其核心问题是 dense prediction 的上下文聚合与分辨率保持。

## Tacit Interpretation

- 很多时候研究者会把“视觉架构史”讲成一条 backbone 越来越强的线，但这会掩盖真正的问题分叉。
- `AlexNet` 在问的是：
  - 视觉深度学习何时真正跨过规模门槛
  - 哪些工程条件必须同时成立
- `Highway -> ResNet` 在问的是：
  - 深层网络怎样能训
  - 信息路径如何设计
- `Dilated Convolutions` 在问的是：
  - dense prediction 应该怎样消费空间信息
  - 上下文与分辨率如何共存
- 所以它们虽然都属于视觉架构论文，但不在同一个主问题上竞争。
- 这意味着后续补资料时，不能只按年代补，而要按“哪条问题线还缺关键断点”来补。

## How To Think

如果一条视觉论文线开始变得混乱，可以先问：

1. 它主要在解决规模化可行性、可训练性，还是任务结构匹配？
2. 它主要改的是信息路径，还是空间几何结构？
3. 它属于 backbone 深化，还是任务特定专用模块？

## How To Apply

- 当前这条视觉分支下一步最该补的，不是随便再来一篇视觉论文，而是按问题线补：
  - `AlexNet -> VGG/BN/Inception`
  - `Highway -> ResNet -> Identity/Pre-activation`
  - `FCN -> Dilated Conv -> DeepLab`

## Links

- [[alexnet]] / [../../concepts/alexnet.md](../../concepts/alexnet.md)
- [[highway-networks]] / [../../concepts/highway-networks.md](../../concepts/highway-networks.md)
- [[residual-networks]] / [../../concepts/residual-networks.md](../../concepts/residual-networks.md)
- [[dilated-convolutions]] / [../../concepts/dilated-convolutions.md](../../concepts/dilated-convolutions.md)
