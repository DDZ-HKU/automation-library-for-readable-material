# VAE 候选论文与阅读顺序

日期：2026-04-16

## 目标

基于当前已经入库的 `Variational Lossy Autoencoder`，把下一阶段最值得补的论文具体化成一份可执行清单。目标不是列全 VAE 史，而是挑出最能推进当前主题线的材料。

当前主题线的核心问题是：

- latent 到底应该承载什么信息
- 强 decoder 为什么会让 latent 被忽略
- 这究竟是 optimization failure，还是 information allocation 的自然结果

所以候选论文优先围绕三条线选：

1. posterior collapse / latent collapse
2. latent shaping / disentanglement
3. hierarchical latent allocation

## 推荐顺序

### 1. Lagging Inference Networks and Posterior Collapse in Variational Autoencoders

为什么先补：

- 它几乎正中当前最关键缺口：posterior collapse 到底该怎么解释和缓解。
- 和 VLAE 放在一起看，会形成一个清晰对照：
  - VLAE 更强调信息分工与 decoder/latent 职责
  - 这篇更强调 inference dynamics 与训练过程中的滞后问题

它最可能补什么：

- posterior collapse 的更标准问题定义
- inference network lagging 这一路解释
- collapse 是如何在训练动态里发生的

### 2. beta-VAE: Learning Basic Visual Concepts with a Constrained Variational Framework

为什么第二篇补它：

- 它代表另一条非常强的 VAE 线：不是调整 decoder 分工，而是通过 objective 改变 latent 偏好。
- 和 VLAE 对照后，会很清楚地看到两种不同思路：
  - architecture-driven information placement
  - objective-driven disentanglement pressure

它最可能补什么：

- latent 应该如何被约束
- disentanglement 为什么会成为 VAE 社区的重要目标
- 更强 KL 约束的收益和代价

### 3. Understanding Posterior Collapse in Generative Latent Variable Models

为什么第三篇补：

- 当前线里还缺一个更偏解释框架的材料，而不仅是单一修复方法。
- 这篇如果补进来，可以帮助判断：
  - posterior collapse 到底有几类成因
  - 哪些解释属于训练问题
  - 哪些解释属于模型结构或目标函数问题

它最可能补什么：

- collapse 的更系统分类
- 现象解释与方法解释的区分
- 当前 tacit note 是否需要修正或扩展

### 4. Ladder VAE / Hierarchical VAE 代表作

建议方向：

- `Ladder Variational Autoencoders`

为什么第四篇补：

- 当前你已经知道 global vs local 的分工，但还只停在单层 latent。
- hierarchical VAE 代表作会把“哪些信息该进 latent”推进成“哪些信息该进哪一层 latent”。

它最可能补什么：

- 分层 latent allocation
- 多层表征各自承担什么结构
- hierarchy 是否真的比单层 latent 更自然

## 为什么不是先补别的

### 不是先补普通 VAE 教程型材料

因为当前缺口已经不是：

- VAE 是什么
- ELBO 怎么写

而是：

- latent 为什么会不用
- latent 到底该学什么

所以再补基础入门材料的信息增量很低。

### 不是先补更强 likelihood 的大模型

如果下一篇只是“更强生成结果”，但不回答：

- collapse 怎么理解
- latent allocation 怎么设计

那对当前分支推进会比较弱。

### 不是先补一堆技巧论文

当前更需要的是先建立问题地图，再看技巧怎么落点。

否则会很快陷入：

- KL annealing
- free bits
- decoder weakening
- skip connections

这些 patchwork 技巧，但缺少统一判断框架。

## 最优执行顺序

如果只能补 2 篇，最稳顺序是：

1. `Lagging Inference Networks and Posterior Collapse in Variational Autoencoders`
2. `beta-VAE`

如果能补 4 篇，最稳顺序是：

1. `Lagging Inference Networks and Posterior Collapse in Variational Autoencoders`
2. `beta-VAE`
3. `Understanding Posterior Collapse in Generative Latent Variable Models`
4. `Ladder Variational Autoencoders`

## 一句话建议

当前最优 next step 不是再随便找一篇 VAE 论文，而是优先找一篇专门讲 posterior collapse 的代表材料；最推荐先找 `Lagging Inference Networks and Posterior Collapse in Variational Autoencoders`。
