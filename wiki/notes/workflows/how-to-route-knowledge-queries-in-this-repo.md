---
title: How to Route Knowledge Queries in This Repo
updated: 2026-04-14
status: active
---

# Summary

这个仓库的知识查询不应从 `raw/` 开始，也不应默认把 `wiki/`、`notes/`、`outputs/` 当成并列入口。最稳的做法是按问题类型路由：先判断这是在问显性知识、默会判断、现成产物，还是需要回到原始资料补洞。这样可以减少重复综合，也能避免明明已有高价值页面却还从零开始读原料。

## Confirmed Understanding

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md) 已确认，非平凡问题默认先读 `wiki/INDEX.md`，优先基于已有 wiki 回答，wiki 不足时再回 `raw/`。
- [.codex/skills/kb-wiki-first/SKILL.md](/Users/ddz/Documents/exp/.codex/skills/kb-wiki-first/SKILL.md) 已确认，知识任务的默认顺序是：
  - `wiki/INDEX.md`
  - relevant `wiki/` pages
  - relevant `outputs/`
  - `raw/` only if the wiki is insufficient
- [how-to-promote-outputs-into-frameworks-or-workflows.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md) 已确认，`outputs/` 不是 disposable chat transcript，而是可复用产物层。
- [tacit-knowledge-layer.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/tacit-knowledge-layer.md) 已确认，`wiki/notes/` 的职责是承接判断框架、应用方法和 tacit interpretation。

## Query Types

先把问题分成 4 类：

### 1. 显性知识问题

典型形式：

- 这是什么
- 有什么区别
- 当前主题线已经确认了什么

首选入口：

- `wiki/concepts/`
- `wiki/sources/`

### 2. 默会判断问题

典型形式：

- 应该怎么理解
- 应该怎么判断
- 这条线真正教会了我们什么

首选入口：

- `wiki/notes/frameworks/`
- `wiki/notes/cases/`

### 3. 现成产物问题

典型形式：

- 先看哪份 output
- 讲懂这份 memo
- 有没有已经写好的相关结果

首选入口：

- `outputs/`
- 与之相关的 `wiki/notes/`

### 4. 补洞问题

典型形式：

- wiki 明显没有覆盖
- 现有页面互相矛盾
- 需要核对原始资料细节

首选入口：

- `raw/`

但前提是：

- 先确认 `wiki/` 和 `outputs/` 确实不足

## Default Routing Order

一个最稳的默认顺序是：

1. 先读 `wiki/INDEX.md`
2. 定位相关 `concepts` / `sources`
3. 如果问题要求判断、应用或高层解释，再转向 `notes/`
4. 如果问题明显在找现成回答或现成产物，再查 `outputs/`
5. 只有当上述层都不足时，再回 `raw/`

## How To Choose Between Notes and Outputs

这是当前最容易混淆的地方。

### 先看 `notes/`

如果用户在问：

- 方法
- 判断
- 框架
- 应用
- 教会我怎么思考

这类问题通常优先看 `notes/`。

### 先看 `outputs/`

如果用户在问：

- 有没有现成答案
- 哪份 memo 最相关
- 讲解一个具体产物
- 这类问题之前有没有已经写过

这类问题通常优先看 `outputs/`。

### 两者都相关时

最稳的顺序是：

1. 先看最相关的 `output`
2. 再用相关 `notes/` 提供更高层解释

## How To Choose Between Frameworks and Cases

### 先看 `frameworks`

如果问题要的是：

- 可迁移方法
- 通用判断模板
- 跨主题可复用框架

### 先看 `cases`

如果问题要的是：

- 某条主题线里的具体解读
- 为什么这条演化线重要
- 某个主题分支的 tacit lesson

### 两者都可能相关时

最稳的顺序是：

1. 先看相关 case，确认具体主题线
2. 再看 framework，把它迁移成更一般的判断

## When To Go Back to Raw

只有出现下面情况之一，才应优先回 `raw/`：

- 现有 wiki 明显没覆盖
- 现有页面互相冲突，需要查一手材料
- 问题依赖原始表述、原始数据或原始上下文
- 新资料刚进入 `raw/inbox/`，还没完成 ingest

不要因为“raw 更原始”就默认先看 raw。

## Minimal Query Flow

一个最小查询流程可以压成这样：

1. 先看 `wiki/INDEX.md`
2. 判断问题属于显性知识、默会判断、现成产物，还是补洞
3. 进入对应首选层：
   - `concepts/sources`
   - `notes`
   - `outputs`
4. 如当前层不足，再向下一层扩展
5. 必要时才回 `raw/`
6. 回答时显式区分：
   - 已确认内容
   - 新增信息
   - 待验证推断

## Common Mistakes

- 还没查 `wiki/` 就先查 `raw/`
- 该看 `notes` 的问题只看了 `concepts`
- 该看 `outputs` 的问题又从零重写一遍
- 把 `frameworks` 和 `cases` 当成同一层
- 没确认 wiki 是否不足，就直接回一手资料

## Source Trace

这页主要由以下规则与页面收束而来：

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md)
- [.codex/skills/kb-wiki-first/SKILL.md](/Users/ddz/Documents/exp/.codex/skills/kb-wiki-first/SKILL.md)
- [tacit-knowledge-layer.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/tacit-knowledge-layer.md)
- [implicit-conventions-audit-2026-04-14.md](/Users/ddz/Documents/exp/outputs/implicit-conventions-audit-2026-04-14.md)

## Links

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md)
- [.codex/skills/kb-wiki-first/SKILL.md](/Users/ddz/Documents/exp/.codex/skills/kb-wiki-first/SKILL.md)
- [tacit-knowledge-layer.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/tacit-knowledge-layer.md)
- [implicit-conventions-audit-2026-04-14.md](/Users/ddz/Documents/exp/outputs/implicit-conventions-audit-2026-04-14.md)
