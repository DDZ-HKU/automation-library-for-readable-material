---
title: Dense Prediction vs Classification Architecture
updated: 2026-04-11
status: active
---

# Summary

`Dilated Convolutions` 这条线真正教会人的，不只是一个卷积技巧，而是一条更通用的判断：当任务目标从“整图一个标签”变成“每个位置都要正确”，很多从 classification 继承来的结构就不再天然合理。dense prediction 会迫使我们重新判断 receptive field、resolution 和 context aggregation 的取舍。

## Confirmed Understanding

- [[multi-scale-context-aggregation-by-dilated-convolutions]] / [../../sources/multi-scale-context-aggregation-by-dilated-convolutions.md](../../sources/multi-scale-context-aggregation-by-dilated-convolutions.md) 明确指出 dense prediction 与 image classification 的结构目标不同。
- 同一来源页确认，dense prediction 的核心矛盾是：既要 multi-scale contextual reasoning，又要 full-resolution output。
- [[dilated-convolutions]] / [../../concepts/dilated-convolutions.md](../../concepts/dilated-convolutions.md) 已确认，dilated convolution 的价值是在不降低分辨率的前提下扩张 receptive field。
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md) 也已确认，这类工作更偏 task-structure-driven architecture，而不是纯优化问题。

## Tacit Interpretation

- classification 架构默认相信：中间分辨率可以不断牺牲，因为最终只需要一个全局判断。
- dense prediction 则要求：局部位置始终重要，不能把空间精度一路压扁到最后再奢望完全恢复。
- 所以同样是“想看更大上下文”，classification 倾向于：
  - pooling
  - stride
  - subsampling
  - 最后全局聚合
- dense prediction 更关心的是：
  - 不丢位置
  - 仍看大范围
  - 让上下文进入每个像素决策
- 这说明架构设计不能只问“什么 backbone 更强”，还要问“任务到底如何消费空间信息”。
- `dilated convolution` 的历史意义就在这里：它提醒我们，很多结构不是“网络越深越对”，而是“网络与任务几何结构是否匹配”。

## What This Teaches

- 一篇架构论文的重要性，有时不在新算子本身，而在它重新定义了什么才算是“合理的结构问题”。
- dense prediction 这类任务会逼迫研究者承认：
  - 分类网络并不是所有视觉任务的默认母体
  - 任务结构本身就应该驱动架构
- 所以读视觉模型论文时，要把“它解决的是 backbone 规模问题”与“它解决的是任务结构匹配问题”分开。

## How To Think

遇到视觉模型时，可以先问：

1. 最终目标是全局标签，还是位置级输出？
2. 中间特征图分辨率被牺牲后，真的能可靠恢复吗？
3. 模型需要的是更大感受野，还是更好地保留空间几何？
4. 所谓“更强 backbone”是不是只是把 classification 假设继续延长？
5. 这篇工作动的是通用 backbone，还是任务特定结构？

## How To Apply

- 读 segmentation / detection / dense prediction 论文时，不要只看它借了哪个分类 backbone，更要看它如何处理 `context vs resolution`。
- 做研究规划时，如果任务本质是位置级决策，优先怀疑分类遗留结构里哪些组件其实是 vestigial。
- 做系统整理时，可以把视觉模型按任务结构分成：
  - classification-first
  - dense-prediction-first

## To Be Verified

- 当前这条解读主要建立在 dilated convolution 论文上，尚未系统纳入 FCN、DeepLab、SegNet 等更完整 dense prediction 脉络。
- 关于“classification 继承部件哪些最常成为 dense prediction 的负担”，还需要更多材料来细化。

## Links

- [[multi-scale-context-aggregation-by-dilated-convolutions]] / [../../sources/multi-scale-context-aggregation-by-dilated-convolutions.md](../../sources/multi-scale-context-aggregation-by-dilated-convolutions.md)
- [[dilated-convolutions]] / [../../concepts/dilated-convolutions.md](../../concepts/dilated-convolutions.md)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [../frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](../frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md)
