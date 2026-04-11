---
title: Complextropy
aliases:
  - first-law-of-complexodynamics
  - sophistication-based-complexity
tags:
  - complexity
  - entropy
  - kolmogorov-complexity
  - physics
updated: 2026-04-08
source_count: 1
status: active
---

# Summary

Complextropy 是 Aaronson 在文章里为“不同于熵、在中间阶段达到峰值的复杂性”提出的临时名称，核心思路是用带资源约束的 sophistication 来刻画“既不简单也不纯随机”的结构性复杂。

## Current Understanding

- 熵衡量的是系统向更典型、更随机状态演化的趋势，但这不足以表示“有趣性”。
- 直觉上，复杂性在低熵初态和高熵终态都较低，在中间混合阶段较高。
- 普通 Kolmogorov complexity 不适合作为该复杂性的定义，因为确定性演化可被非常短的程序描述。
- 不带资源约束的 sophistication 仍会低估复杂性，因为“可达状态集合”本身可被简洁描述。
- 更合理的候选量是带资源约束的 sophistication：同时限制采样程序和重建程序的计算效率。

## Evidence

- 主要依据来自 [[the-first-law-of-complexodynamics]] / [../sources/the-first-law-of-complexodynamics.md](../sources/the-first-law-of-complexodynamics.md)。
- 典型直觉案例是咖啡和牛奶混合：分离态和完全均匀态都较简单，中间边界最丰富的状态更复杂。

## Open Questions

- 是否能在某个具体离散动力系统中严格证明 complextropy 呈现“小 - 大 - 小”曲线？
- 哪种资源约束最自然：时间界、空间界还是电路复杂度界？
- 经验近似时，gzip 之类的压缩指标是否足够反映这种“结构性复杂”？

## Related Pages

- [[the-first-law-of-complexodynamics]] / [../sources/the-first-law-of-complexodynamics.md](../sources/the-first-law-of-complexodynamics.md)
- [[llm-wiki]] / [llm-wiki.md](llm-wiki.md)
