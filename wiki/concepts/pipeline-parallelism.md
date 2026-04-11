---
title: Pipeline Parallelism
aliases:
  - micro-batch-pipeline-parallelism
  - model-pipeline-parallelism
tags:
  - deep-learning
  - systems
  - distributed-training
updated: 2026-04-09
source_count: 1
status: active
---

# Summary

Pipeline parallelism 是一种训练超大模型的系统方法：把按层顺序排列的网络切成多个连续分区，分别放到不同设备上，再把一个 mini-batch 切成多个 micro-batches，让不同设备像流水线一样并行处理这些微批次。

## Current Understanding

- 它的目标是突破单设备内存限制，让更深或更宽的模型能够被训练。
- 这种方法特别适合可以自然表示成“层序列”的网络，如深层 Transformer 或卷积网络。
- micro-batch 是流水线效率的关键调节杆：太少会导致设备空转，太多则会引入额外调度和状态管理成本。
- GPipe 代表的是同步式 pipeline parallelism：先在多个 micro-batches 上累积梯度，再统一更新参数。
- re-materialization 与 pipeline parallelism 常一起出现，因为它们共同服务于“用更多计算换更低内存占用”。
- 与纯数据并行相比，它关注的是拆模型；与张量并行/SPMD 相比，它更强调沿层深方向切分。

## Evidence

- 当前主要依据来自 [[gpipe-easy-scaling-with-micro-batch-pipeline-parallelism]] / [../sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md](../sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md)。
- 它补充了 [[transformers]] / [transformers.md](transformers.md) 中尚未展开的一个现实层面问题：Transformer 不只需要好架构，还需要可扩展的训练系统。

## Open Questions

- 在今天的超大模型训练里，pipeline parallelism 与 tensor parallelism、data parallelism 的最佳组合边界是什么？
- 同步式与异步式 pipeline 在稳定性、吞吐与实现复杂度上的权衡该如何总结？
- 从 GPipe 到后续 Megatron、DeepSpeed 等系统，哪些是延续，哪些是关键改进？

## Related Pages

- [[gpipe-easy-scaling-with-micro-batch-pipeline-parallelism]] / [../sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md](../sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md)
- [[transformers]] / [transformers.md](transformers.md)
