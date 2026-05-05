---
title: How to Write a Stage Research Decision Memo
updated: 2026-04-13
status: active
---

# Summary

当一个主题线已经积累了若干资料，但还没准备进入下一轮 ingest 时，最稳的做法不是立刻继续加材料，而是先写一份阶段研究决策 memo。它的作用不是重复总结已知内容，而是压缩当前判断、指出关键缺口、排出下一步阅读顺序，并明确哪些方向暂时不值得补。

## Confirmed Understanding

- `outputs/rnn-next-research-directions-2026-04-08.md` 已展示，这类 memo 应把“当前已知什么”和“下一阶段该读什么”分开。
- `outputs/rnn-transformer-research-decision-memo-2026-04-09.md` 已展示，好的决策 memo 会明确：
  - 当前最稳的判断
  - 当前最大的缺口
  - 不建议继续补的方向
  - 推荐阅读顺序
- `outputs/vision-architecture-next-research-directions-2026-04-11.md` 已展示，这类 memo 还应指出：
  - 当前知识线已经分成哪些子线
  - 哪个 next step 最能把分支补闭合
- [[how-to-turn-paper-reading-into-research-decisions]] / [../frameworks/how-to-turn-paper-reading-into-research-decisions.md](../frameworks/how-to-turn-paper-reading-into-research-decisions.md) 已确认，读完材料后必须把理解压缩成后续研究动作，而不能只停在“我懂了”。

## When To Use

在以下情况应写阶段研究决策 memo：

- 一个主题线已经完成一轮 ingest
- 当前已有若干来源和概念页，但下一步阅读方向不再显然
- 你需要暂停当前分支，并让未来可以无损续接
- 你需要在多个可能 next step 中做优先级取舍

## What This Memo Is For

这类 memo 主要解决 4 个问题：

1. 当前主题线最稳的判断是什么？
2. 现在真正缺的是什么，而不是还能再补什么？
3. 接下来最该读哪几类材料，顺序怎么排？
4. 哪些方向暂时不该优先？

## Memo Structure

一份最小可用的阶段研究决策 memo，建议至少包含下面几段：

### 1. 当前状态

写清楚当前主题线已经具备哪些关键材料和判断。

不要只是列文件名，要说明：

- 这些材料分别回答了什么问题
- 当前知识线已经形成了哪些子线

### 2. 当前最稳的判断

压缩出 3 到 4 条当前最值得保留的判断。

这些判断应是：

- 已经相对稳定
- 足以指导下一步选材
- 不是临时 impression

### 3. 当前缺口

明确当前最重要的空白是什么。

不要写成“还能补很多”，而要写成：

- 缺哪类材料
- 为什么这是主缺口
- 如果不补，会导致哪条理解停在半路

### 4. 不建议继续补的方向

这部分很重要。

它的作用是：

- 防止下一轮阅读被泛泛材料带偏
- 明确当前阶段哪些资料即使有价值，也不是现在最优先

### 5. 接下来最该补的材料

把后续材料按类型列出，而不只是给论文名。

例如：

- 一篇瓶颈总结材料
- 一篇桥梁材料
- 一篇系统扩展材料

### 6. 推荐阅读顺序

把 next step 排成 1, 2, 3。

顺序必须解释原因，而不是只给列表。

### 7. 一句话行动建议

最后用一句话压缩：

- 下一步最该干什么
- 当前最不该浪费时间在哪

## Writing Flow

写这类 memo 时，按下面流程进行：

1. 回看当前主题线已有的 `sources`、`concepts`、`notes/cases`
2. 压缩出当前最稳的判断
3. 判断真正主缺口在哪，而不是列所有可能缺口
4. 列出 2 到 4 类最该补的材料
5. 排出推荐阅读顺序
6. 补一段“不建议继续补的方向”
7. 把结果保存到 `outputs/`

## How To Judge Quality

一份好的阶段研究决策 memo，应满足：

- 读者能立即知道当前分支卡在哪里
- 读者能立即知道下一篇最该补什么
- 读者能知道哪些方向先别碰
- 未来恢复这条分支时，不需要重读全部历史材料

## Common Mistakes

- 把 memo 写成阶段总结，导致缺少决策性
- 只列“可补材料清单”，不判断主缺口
- 不写“不建议继续补的方向”，导致后续优先级发散
- 给出阅读顺序，但不解释为什么这个顺序成立

## Source Trace

这页主要由以下 outputs 提炼而来：

- [../../../outputs/rnn-next-research-directions-2026-04-08.md](../../../outputs/rnn-next-research-directions-2026-04-08.md)
- [../../../outputs/rnn-transformer-research-decision-memo-2026-04-09.md](../../../outputs/rnn-transformer-research-decision-memo-2026-04-09.md)
- [../../../outputs/vision-architecture-next-research-directions-2026-04-11.md](../../../outputs/vision-architecture-next-research-directions-2026-04-11.md)

## Links

- [[how-to-turn-paper-reading-into-research-decisions]] / [../frameworks/how-to-turn-paper-reading-into-research-decisions.md](../frameworks/how-to-turn-paper-reading-into-research-decisions.md)
- [[research-reading-and-decision-stack]] / [../frameworks/research-reading-and-decision-stack.md](../frameworks/research-reading-and-decision-stack.md)
- [../../../outputs/rnn-transformer-research-decision-memo-2026-04-09.md](../../../outputs/rnn-transformer-research-decision-memo-2026-04-09.md)
