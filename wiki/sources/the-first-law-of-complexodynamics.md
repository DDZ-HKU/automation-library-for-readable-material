---
title: The First Law of Complexodynamics
source_path: raw/The First Law of Complexodynamics.md
source_type: blog-post
author: Scott Aaronson
published: 2011-09-24
processed: 2026-04-08
topics:
  - complextropy
  - sophistication
  - kolmogorov-complexity
  - entropy
entities:
  - Scott Aaronson
  - Sean Carroll
status: active
---

# Summary

Scott Aaronson 在这篇文章中尝试解释一个现象：物理系统的熵通常单调上升，但“复杂性/有趣性”往往是在中间阶段达到峰值，并提出可用带资源约束的 algorithmic sophistication 来刻画这种中间态复杂性。

## Core Claims

- 熵的上升并不能直接解释“为什么系统在中间阶段看起来最复杂”。
- 普通的 Kolmogorov complexity 不能很好刻画这种现象，因为在确定性系统中状态常可由“初态 + 演化步数”简短描述。
- 不带资源约束的 sophistication 也不足以解释该现象，因为可通过“可达状态集合”把复杂度压到很低。
- 一个更可行的方向是引入双重资源约束：既限制生成集合样本的程序效率，也限制在给定该集合样本时重建目标状态的程序效率。
- 作者猜想，在这种定义下，复杂性会呈现“小 - 大 - 小”的动态曲线，即所谓的 “First Law of Complexodynamics”。

## Key Facts

- 文章围绕 Sean Carroll 提出的问题展开：为什么复杂性不像熵那样单调，而是先升后降。
- Aaronson 用咖啡和牛奶混合的例子说明：最初分离、最终均匀混合的状态都不如中间的涡流边界复杂。
- 文章把 “复杂性” 临时命名为 `complextropy`，以免与其他复杂度概念混淆。
- 讨论的理论工具包括 Kolmogorov complexity、sophistication、Kolmogorov structure functions 和 algorithmic statistics。
- 作者建议用离散化的“咖啡杯”模型做理论或经验研究，例如二维黑白像素格的随机混合过程。
- 文章指出 complextropy 的精确计算大概率不可 tractable，但可以用 gzip 压缩率之类的代理指标做经验近似。

## Tensions / Contradictions

- 文章提出的是研究猜想和方向，不是已证明定理。
- 直觉上“中间态最复杂”很强，但严格数学证明尚未给出。
- 普通 Kolmogorov complexity 与直觉复杂性之间存在明显错位：随机串虽然高 Kolmogorov complexity，却通常不被认为“有趣”。

## Links Into Wiki

- [[complextropy]] / [../concepts/complextropy.md](../concepts/complextropy.md)
- [[llm-wiki]] / [../concepts/llm-wiki.md](../concepts/llm-wiki.md)
