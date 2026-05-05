# VAE 目标论文清单

日期：2026-04-16

## 用法

这份清单不是综述，而是一个“下次直接丢 PDF”用的短名单。你后面只要按这里的顺序把论文文件放进来，我就能直接沿当前 VAE 分支继续接，不需要再临时判断优先级。

## Priority 1

### Lagging Inference Networks and Posterior Collapse in Variational Autoencoders

- 作用：当前最关键的一篇，用来正式补 `posterior collapse` 主问题
- 位置：`collapse` 簇
- 标识：`arXiv:1901.05534`
- 入口：
  - https://openreview.net/forum?id=rylDfnCqF7
  - https://dblp.org/rec/journals/corr/abs-1901-05534

为什么先补：

- 它最直接回答当前分支最大的缺口：latent 为什么会不用
- 它会和 `VLAE` 形成最关键对照：
  - `VLAE`：information preference / allocation
  - `Lagging Inference`：training dynamics / inference lag

## Priority 2

### beta-VAE: Learning Basic Visual Concepts with a Constrained Variational Framework

- 作用：补 `latent shaping / disentanglement` 主线
- 位置：`shaping` 簇
- 稳定入口：
  - https://openreview.net/forum?id=Sy2fzU9gl

为什么第二篇补：

- 它代表另一种完全不同的答案：
  - 不是通过 decoder 分工决定 latent 学什么
  - 而是通过 objective 约束 latent 偏好

## Priority 3

### Understanding Posterior Collapse in Generative Latent Variable Models

- 作用：补一个更偏解释框架的 collapse 材料
- 位置：`collapse` 簇
- 稳定入口：
  - https://openreview.net/forum?id=r1xaVLUYuE
  - https://dblp.org/rec/conf/iclr/LucasTGN19

为什么第三篇补：

- 它能帮助把 collapse 从“某篇论文的说法”推进成更系统的问题解释
- 适合在 `Lagging Inference` 之后读，用来判断 collapse 的多种成因

## Priority 4

### Ladder Variational Autoencoders

- 作用：补 `hierarchical latent allocation` 主线
- 位置：`hierarchy` 簇
- 标识：`arXiv:1602.02282`
- 入口：
  - https://papers.nips.cc/paper/6275-ladder-variational-autoencoders
  - https://www.emergentmind.com/articles/1602.02282

为什么第四篇补：

- 当前 VAE 分支已经知道 global vs local 的单层分工
- 这篇会把问题推进成：不同层 latent 各自应该学什么

## 建议文件投喂顺序

最短顺序：

1. `1901.05534`
2. `beta-VAE`

完整顺序：

1. `1901.05534`
2. `beta-VAE`
3. `Understanding Posterior Collapse in Generative Latent Variable Models`
4. `1602.02282`

## 一句话建议

如果你现在只准备继续一篇，优先找并丢进来的是：`Lagging Inference Networks and Posterior Collapse in Variational Autoencoders`。
