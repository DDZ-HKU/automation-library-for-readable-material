# Vision Architecture 下一步研究方向

日期：2026-04-11

## 当前状态

目前视觉侧已经形成了四条互补但不同层次的线：

1. `AlexNet`
2. `Highway Networks`
3. `ResNet`
4. `Dilated Convolutions`

它们分别回答的是不同问题：

- `AlexNet`：视觉深度学习为什么第一次在大规模上真正成立
- `Highway Networks`：极深网络怎样保持可训练性
- `ResNet`：怎样把优化困难压缩成默认直通 + 残差修正
- `Dilated Convolutions`：dense prediction 怎样扩大上下文而不丢分辨率

所以当前材料并不是同一条单线演化，而是已经开始分成：

- 视觉深度学习的大规模可行性起点
- 深层网络优化与信息路径
- 任务结构驱动的视觉架构

## 当前最稳的四条判断

### 1. AlexNet 是视觉深度学习的规模起点

AlexNet 已经说明：

- 真正的断点不一定是全新理论，而可能是大数据、算力、训练技巧和模型容量第一次被成功组装

### 2. Skip path 这条线不是从 ResNet 凭空开始的

Highway Networks 已经说明，社区在 ResNet 之前就已经意识到：

- 极深网络需要跨层直通路径

### 3. ResNet 的真正强点是“更轻的默认直通”

ResNet 保留了 skip path 的关键思想，但把 gated carry 压成了更轻量的 identity shortcut。

### 4. Dense prediction 不是 classification 的自然尾声

Dilated Convolutions 明确说明：

- dense prediction 会逼出不同于 classification 的架构判断

## 当前缺口

### 1. 缺 ResNet 后续的 identity/pre-activation 材料

当前你已经知道：

- Highway Networks
- ResNet

但还缺：

- identity mapping later variants
- pre-activation 改进

否则 `Highway -> ResNet` 还只停在桥梁阶段，没有看到 ResNet 为什么会被进一步规范化。

### 2. 缺 dense prediction 这条线的更完整母线

现在只有 dilated convolutions，还缺：

- FCN
- DeepLab
- encoder-decoder segmentation 代表作

否则你知道了一种关键结构判断，但还看不到完整任务谱系。

### 3. 缺 AlexNet 到更稳定视觉训练套路的中间规范化材料

现在有了 AlexNet 作为规模起点，但还缺：

- VGG
- BatchNorm 代表作
- Inception

否则你只能看到“深度视觉突然赢了”，还看不到它是怎样被整理成稳定方法论的。

### 4. 缺视觉架构与后来的 attention/Transformer 视觉化过渡

如果你以后要把视觉线接到更大的“架构如何变化”问题，就还缺：

- vision transformers
- attention 在视觉里的结构动机

## 下一篇最该补什么

### 优先级 1

补 `Identity Mappings in Deep Residual Networks`

原因：

- 它能直接回答 ResNet 为什么不是终点
- 能把 Highway -> ResNet -> pre-activation 这条线补闭合

### 优先级 2

补 `Fully Convolutional Networks for Semantic Segmentation`

原因：

- 这样 dilated conv 才有更明确的前文
- 能更清楚看到“classification adaptation -> dense prediction specialization”的差异

### 优先级 3

补 `VGG` 或 `BatchNorm` 代表作

原因：

- 把 AlexNet 的规模突破过渡成更系统的视觉训练套路

### 优先级 4

补一篇 `DeepLab` 代表作

原因：

- 可以把 dilated conv 从“单篇关键技巧”升级为“Dense Prediction 主线中的稳定结构”

## 一句话建议

如果继续沿当前视觉分支推进，最优顺序是：

1. `Identity Mappings in Deep Residual Networks`
2. `Fully Convolutional Networks for Semantic Segmentation`
3. `VGG` 或 `BatchNorm` 代表作
4. 一篇 `DeepLab` 代表作

这样你会同时补齐：

- AlexNet 之后的视觉主线规范化
- skip/residual path 的后续规范化
- dense prediction 架构主线

## Recommended Reading Order

1. `Identity Mappings in Deep Residual Networks`
2. `Fully Convolutional Networks for Semantic Segmentation`
3. `VGG` 或 `BatchNorm` 代表作
4. 一篇 `DeepLab` 代表作

## Next Step

当前最优 next step 是补 `Identity Mappings in Deep Residual Networks` 或 `Fully Convolutional Networks for Semantic Segmentation` 中的一篇，以便沿现有视觉分支继续推进。

## Next Autonomous Move

默认情况下，next autonomous move 应是：`wait for a new PDF`，优先等待 `Identity Mappings in Deep Residual Networks` 或 `Fully Convolutional Networks for Semantic Segmentation` 的文件进入项目。

如果不等待新论文，也可以 `switch to a different staged paper`，但那会偏离当前最优视觉分支顺序。
