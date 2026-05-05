---
title: Relational Memory Core
aliases:
  - rmc
tags:
  - recurrent-neural-networks
  - attention
  - relational-reasoning
updated: 2026-04-16
source_count: 1
status: active
---

# Summary

RMC 是一种把 multi-head attention 嵌入 memory 内部的 recurrent 结构，用来让记忆槽位彼此交互、组合和推理。它的重点不是“更长记忆”，而是“记忆内部的关系计算”。

## Current Understanding

- 普通 RNN / memory 模型更擅长状态累积，不一定擅长 relational reasoning。
- RMC 通过 memory-to-memory attention，让记忆本身成为一个可交互的关系场。
- 这使模型从单一隐状态更新，推进到多个 slot 的关系运算。

## Evidence

- 当前主要依据来自 [[relational-recurrent-neural-networks]] / [../sources/relational-recurrent-neural-networks.md](../sources/relational-recurrent-neural-networks.md)。

## Related Pages

- [[relational-recurrent-neural-networks]] / [../sources/relational-recurrent-neural-networks.md](../sources/relational-recurrent-neural-networks.md)
- [[recurrent-neural-networks]] / [recurrent-neural-networks.md](recurrent-neural-networks.md)
