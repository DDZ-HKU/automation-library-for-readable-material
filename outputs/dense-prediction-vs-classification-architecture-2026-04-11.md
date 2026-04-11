# Dense Prediction 为什么会逼出不同于 Classification 的架构

日期：2026-04-11

## 结论

`Dilated Convolutions` 这篇论文真正重要的地方，不只是提出了一个算子，而是明确提出：

- semantic segmentation 这类 dense prediction 任务
- 与 image classification 的结构目标不同

所以你不能默认：

- classification backbone 只要稍改一下
- 就自然适合 dense prediction

## 核心差异

classification 的默认目标是：

- 整张图最后给一个全局判断

这意味着中间过程里：

- 分辨率可以一路降
- pooling 和 stride 很自然
- 最终只要全局语义强就行

dense prediction 的目标则是：

- 每个位置都要做判断

这意味着模型必须同时满足：

- 看足够大的上下文
- 又不能丢掉位置精度

## 为什么这会逼出新架构

因为 classification 的常见解决方案是：

- 不断下采样
- 用更深层获得更大感受野
- 最后再做全局聚合

但 dense prediction 不能轻易接受这套默认假设。

如果空间分辨率在中间被严重牺牲，那么：

- 后面再恢复
- 并不总是可靠

所以 dense prediction 架构更关心的不是“怎么把 feature 做得更抽象”，而是：

- 怎么在保留分辨率的同时扩大感受野

## Dilated Convolution 的真正价值

它提供的不是单纯“卷积的新变体”，而是一种结构判断：

- 我们不一定非要通过 pooling/downsampling 才能获得更大上下文
- 也可以通过 dilation 扩张 receptive field
- 同时保留 feature map resolution

所以它代表的是一种任务结构驱动的架构设计。

## 一句话理解

classification-first 架构问的是：

- 怎么把整张图压成最强的全局表示

dense-prediction-first 架构问的是：

- 怎么让每个位置在不丢精度的前提下看到足够大的上下文

这就是为什么 dense prediction 会逼出不同于 classification 的架构判断。

## 对研究最重要的提醒

以后读视觉论文时，不要只问：

- 这个 backbone 强不强

还要问：

- 这个任务真正如何消费空间信息
- 哪些 classification 遗留结构其实成了负担
- 这篇论文到底是在扩 backbone，还是在重写任务结构

## 后续沉淀

这条判断已经沉淀为长期默会知识页：

- [dense-prediction-vs-classification-architecture.md](/Users/ddz/Documents/exp/wiki/notes/cases/dense-prediction-vs-classification-architecture.md)
