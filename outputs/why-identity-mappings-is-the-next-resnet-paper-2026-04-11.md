# 为什么下一篇应该是 Identity Mappings in Deep Residual Networks

日期：2026-04-11

## 结论

在当前视觉架构分支里，`Identity Mappings in Deep Residual Networks` 是最合理的下一篇，不是因为它“又是一篇 ResNet 论文”，而是因为它正好回答当前分支最大的剩余问题：

- ResNet 为什么不是 skip/residual 这条线的终点？
- 在 Highway Networks 到 ResNet 之后，社区到底把哪一部分进一步规范化了？

一句话说：

如果 AlexNet 解决的是“深度视觉为什么第一次在规模上成立”，Highway/ResNet 解决的是“深层网络怎么训”，那么 `Identity Mappings...` 解决的就是“ResNet 这条方法论怎样被进一步整理成更稳定的默认结构”。

## 当前分支还缺什么

现在你已经有：

- `AlexNet`
- `Highway Networks`
- `ResNet`
- `Dilated Convolutions`

所以当前视觉分支已经能回答三件事：

1. 深度视觉如何在大规模上第一次成立
2. skip path 为什么成为关键结构
3. dense prediction 为什么逼出不同于 classification 的架构

但还缺一层：

- ResNet 在成为主流默认骨架后，是怎样进一步被“规范化”的

没有这层，你现在只能说：

- Highway 抓住了 gated carry path
- ResNet 抓住了 default pass-through + residual reformulation

但还不能说：

- 为什么社区后来更偏向某种更“干净”的 residual block 组织方式
- pre-activation / identity mapping 为什么会进一步提高稳定性

## 为什么不是先补别的

### 不是先补 DeepLab

DeepLab 属于 dense prediction 主线。

它当然重要，但当前 `Dilated Convolutions` 这条线至少已经有了一个明确的结构判断：

- dense prediction 不该完全继承 classification 的空间处理方式

相比之下，`Highway -> ResNet` 这条线目前还停在：

- 过渡已经补了
- 但后续规范化还没补

所以更缺的是 ResNet 后续。

### 不是先补随机视觉 backbone

如果下一篇只是再补一篇一般视觉 backbone，而没有回答：

- skip/residual path 后来怎样进一步稳定化

那它对当前分支的推进会比较弱。

### 也不是先补 Vision Transformer

那会直接跳到另一代架构断点，当前中间层还没补齐。

## Identity Mappings 这篇会补什么

它最可能补齐四个空白：

1. `identity shortcut` 在更深残差网络里到底扮演什么角色
2. pre-activation 为什么会改善优化与信息流
3. ResNet 之后 community 如何把 residual block 变成更稳定的默认单元
4. 为什么 ResNet 不是单点技巧，而是一条还在继续抽象化的结构路线

## 这篇一旦补上，分支会怎么变化

当前：

- `AlexNet -> Highway -> ResNet`

补完后：

- `AlexNet -> Highway -> ResNet -> Identity/Pre-activation`

这会让 skip/residual 这条线从“桥梁”升级成“闭环中的三段演化”：

- 受控跨层信息流
- 默认直通 + 增量修正
- 更稳定的 identity / pre-activation 组织方式

## 如果现在没有这篇 PDF，该怎么做

如果当前本地没有 `Identity Mappings in Deep Residual Networks` 的 PDF，最稳的下一步不是随便切别的论文，而是：

1. 把它明确标成当前分支的 `next step`
2. 保持当前阶段在这里自然交接
3. 等新 PDF 到位后继续自动运行

## 一句话判断

`Identity Mappings in Deep Residual Networks` 是当前视觉分支最合理的下一篇，因为它正好位于 Highway -> ResNet 之后，负责把“残差路径为什么有效”从一个成功技巧推进成一个更稳定的结构原则。
