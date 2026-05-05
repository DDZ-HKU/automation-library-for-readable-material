---
title: How to Manage Partially Promoted Outputs
updated: 2026-04-14
status: active
---

# Summary

有些 `outputs/` 的核心判断已经回灌到 `wiki/notes/` 或 `wiki/concepts/`，但产物本身仍保留额外的应用展开、比较结构或阶段性上下文。这类对象不该被简单归为“已升格”或“仅保留 output”，而应被视作 `partially promoted outputs`。这页的作用，是定义这类对象该如何识别、如何回链、何时继续收束，避免知识库长期留下边界模糊的半成品状态。

## Confirmed Understanding

- [how-to-promote-outputs-into-frameworks-or-workflows.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md) 已确认，知识产物至少会流向：
  - `outputs`
  - `wiki/notes/frameworks`
  - `wiki/notes/workflows`
  - `wiki/concepts`
- [output-promotion-audit-2026-04-13.md](/Users/ddz/Documents/exp/outputs/output-promotion-audit-2026-04-13.md) 已确认，当前仓库里已经存在一类稳定对象：
  - 核心判断已进入 wiki
  - 但 output 仍保留更长的应用展开
- 当前仓库中典型例子包括：
  - [cli-tool-system-design-from-tool-papers-2026-04-13.md](/Users/ddz/Documents/exp/outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md)
  - [highway-networks-vs-resnet-2026-04-10.md](/Users/ddz/Documents/exp/outputs/highway-networks-vs-resnet-2026-04-10.md)

## What Counts as Partial Promotion

一个 output 可视作 `partially promoted`，当它同时满足下面两点：

1. 核心判断、主题线或方法模板已经进入 `wiki/`
2. output 本身仍保留不可被 wiki 页完全替代的额外价值

这种额外价值通常包括：

- 更长的应用展开
- 更直接的比较写法
- 更适合人类快速回看的 memo 形态
- 面向具体项目或场景的展开映射

## What This State Is For

`partially promoted` 不是失败状态，也不是过渡噪音。

它的合理用途是：

- 让 wiki 承接长期稳定结论
- 让 output 继续承接更具体、更长、更应用化的表达

问题不在于存在这种状态，而在于：

- 没有显式回链
- 没有说明哪部分已经进 wiki
- 没有说明 output 还保留什么独特价值

## Required Handling

对于 `partially promoted output`，至少要做 3 件事：

### 1. 给 output 补 `Source Trace`

output 里要明确写出：

- 哪些核心判断已经回灌到哪个 wiki 页面
- output 现在还保留什么独特价值

### 2. 给对应 wiki 页补上游 output 记录

wiki 页面里要写明：

- 这页的主要上游 output 包括哪些

这样之后再看知识线时，就不会把 wiki 页误以为完全凭空生成。

### 3. 在 audit 中标记为 `部分升格`

不要把这类对象硬塞进“已升格”或“保留 output”。

它们需要单独管理。

## When to Keep the Output

即使已经有对应 wiki 页，只要 output 仍具备下面任一价值，就应继续保留：

- 更适合快速对比
- 更贴近具体项目应用
- 作为长文 memo 更易分发
- 保留了 wiki 页刻意压缩掉的阶段性上下文

## When to Further Collapse It

如果一个 `partially promoted output` 后来出现下面情况，就可以考虑进一步收束：

- output 和 wiki 页内容已经几乎重复
- output 的独特应用价值已经被新的 framework / workflow 吸收
- 读者再看 output 已经拿不到额外信息

这时可以：

- 在 audit 中把它从 `部分升格` 调整为 `已升格`
- 或只保留 output 作为历史留档，不再把它视为活跃入口

## Minimal Workflow

1. 发现一个 output 的核心判断已经进入 wiki
2. 判断 output 是否仍保留独特价值
3. 如果有，标记为 `部分升格`
4. 给 output 补 `Source Trace`
5. 给对应 wiki 页补上游 output 记录
6. 在后续 audit 中持续检查它是否还值得继续保留

## Common Mistakes

- 只补 wiki，不补 output 回链
- 只补 output，不补 wiki 上游记录
- 把部分升格对象误判成“已完全升格”
- 因为怕重复就过早删除 output 的应用展开价值

## How To Apply in This Repo

当前仓库里，最适合按这套流程处理的是：

- 先判断 output 是否已经有对应 `framework`、`workflow` 或 `case`
- 如果已有，但 output 还更适合项目级阅读或比较阅读，就保留为 `部分升格`
- 用双向 `Source Trace` 把关系写明

## Source Trace

这页主要由以下材料收束而来：

- [how-to-promote-outputs-into-frameworks-or-workflows.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md)
- [output-promotion-audit-2026-04-13.md](/Users/ddz/Documents/exp/outputs/output-promotion-audit-2026-04-13.md)
- [implicit-conventions-audit-2026-04-14.md](/Users/ddz/Documents/exp/outputs/implicit-conventions-audit-2026-04-14.md)

## Links

- [how-to-promote-outputs-into-frameworks-or-workflows.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md)
- [output-promotion-audit-2026-04-13.md](/Users/ddz/Documents/exp/outputs/output-promotion-audit-2026-04-13.md)
- [implicit-conventions-audit-2026-04-14.md](/Users/ddz/Documents/exp/outputs/implicit-conventions-audit-2026-04-14.md)
