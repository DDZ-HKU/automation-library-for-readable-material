# VAE 最短阅读路径

日期：2026-04-16

## 适用场景

这份路径适合现在这种状态：

- 你刚开了 VAE 分支
- 已有 `VLAE` 一篇核心材料
- 想快速进入真正的问题主线，而不是先掉进大量技巧或模型名里

## 最短路径

### 第 1 步

先看：

- [../wiki/sources/variational-lossy-autoencoder.md](../wiki/sources/variational-lossy-autoencoder.md)

目的：

- 建立当前分支的起点
- 明确 `latent vs decoder` 的信息分工问题

### 第 2 步

再看：

- [../wiki/concepts/variational-autoencoders.md](../wiki/concepts/variational-autoencoders.md)

目的：

- 把单篇论文的判断提升成当前主题理解
- 明确 VAE 主问题已经从“形式定义”转到 “latent allocation”

### 第 3 步

再看：

- [../wiki/notes/cases/how-to-think-about-decoder-strength-and-latent-usefulness-in-vaes.md](../wiki/notes/cases/how-to-think-about-decoder-strength-and-latent-usefulness-in-vaes.md)

目的：

- 把“强 decoder 导致 latent 无用”的直觉改写成“信息分工”的判断

### 第 4 步

再看：

- [../wiki/notes/frameworks/how-to-map-vae-papers-by-latent-allocation-problem.md](../wiki/notes/frameworks/how-to-map-vae-papers-by-latent-allocation-problem.md)

目的：

- 拿到后续读 VAE 论文的路由框架
- 先按 `collapse / shaping / hierarchy / stabilization` 分类，再决定要不要深入

### 第 5 步

最后看：

- [vae-next-research-directions-2026-04-16.md](vae-next-research-directions-2026-04-16.md)
- [vae-candidate-papers-and-reading-order-2026-04-16.md](vae-candidate-papers-and-reading-order-2026-04-16.md)

目的：

- 明确下一批最值得补的论文
- 直接把这条线推进到下一篇材料

## 一句话版本

如果只看三份，最稳顺序是：

1. `variational-lossy-autoencoder`
2. `variational-autoencoders`
3. `how-to-think-about-decoder-strength-and-latent-usefulness-in-vaes`

## 当前最优 next step

读完上面路径后，直接补一篇 `posterior collapse` 代表材料，不要先补泛泛的 VAE 入门文或技巧 patch 文。
