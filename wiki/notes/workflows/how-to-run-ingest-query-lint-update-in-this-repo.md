---
title: How to Run Ingest Query Lint Update in This Repo
updated: 2026-05-05
status: active
---

# Summary

这个仓库最稳定的运行方式，不是把知识工作混成一种模糊的“整理”，而是明确分成 `Ingest`、`Query`、`Lint`、`Update` 四种模式。四者共享同一个三层结构：`raw/` 保留原始资料，`wiki/` 保存提炼后的长期知识，`outputs/` 保存可复用的阶段产物。它们的区别不在目录，而在目标、输入、输出和允许的变更方式不同。

## Confirmed Understanding

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md) 已确认，仓库的总原则是原始资料不改写、优先复用已有 wiki、结果有长期价值时沉淀到 `outputs/` 或 `wiki/notes/`。
- [README.md](/Users/ddz/Documents/exp/README.md) 已确认，当前仓库采用 `raw / wiki / outputs` 三层结构，并把知识维护视为持续编译过程，而非临时检索。
- [how-to-route-knowledge-queries-in-this-repo.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-route-knowledge-queries-in-this-repo.md) 已确认，查询时默认先走 wiki-first 路由，只在 wiki 不足时回到原始资料。
- [how-to-promote-outputs-into-frameworks-or-workflows.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md) 已确认，`outputs/` 是可复用产物层，不是一次性聊天残留。

## 1. Ingest

目标：

- 把散落的原始页面提炼成结构化话题页
- 去重、结构化、精确化
- 让后续查询不必每次回到原文重做综合

常见输入：

- `raw/` 中的新 Markdown、PDF、网页剪藏、Confluence 导出页
- `raw/inbox/` 中尚未进入 `raw/sources/` 的资料

核心要求：

- 不搬运大段原文
- 同主题多份资料先找共同结构，再决定如何拆页
- 原始资料保留在 `raw/`，提炼结果进入 `wiki/sources/`、`wiki/concepts/`、`wiki/notes/`

最小流程：

1. 识别资料类型、主题、作者、日期、来源
2. 抽出核心论点、事实、争议和关键数据
3. 去重并压缩成更稳定的主题结构
4. 写或更新 `wiki/sources/`
5. 写或更新相关 `wiki/concepts/` / `wiki/notes/`
6. 更新 `wiki/INDEX.md`、`wiki/overview.md`、`wiki/log.md`

## 2. Query

目标：

- 用尽量少的阅读量给出高质量回答
- 优先复用已合成知识，而不是从零综合
- 让答案保持来源可追溯

核心原则：

- 两路并发检索：
  - 已合成的 `wiki/` / `outputs/`
  - 对应的 `raw/` 原始资料
- 但回答时是“合成优先、原文补充”，不是两边平权

适用判断：

- `wiki/` 负责精炼、稳定、跨资料整合后的知识
- `raw/` 负责原始表述、原始上下文、细节核对和冲突校验

回答要求：

- 优先引用 `wiki/concepts/`、`wiki/sources/`、`wiki/notes/`
- 原始资料只在必要时补充
- 每条关键信息尽量指回来源摘要页或原始来源

## 3. Lint

目标：

- 定期暴露知识库结构性问题
- 先输出健康报告，再决定是否修复

至少检查 3 类核心问题：

- 断链：
  - 来源页、来源摘要页、交叉引用是否失效
- 过期：
  - 超过 90 天未更新且仍在高频使用的页面
- 孤儿页：
  - 页面存在，但未进入 `wiki/INDEX.md` 或未被高价值入口挂上

同时继续检查：

- 页面之间的矛盾
- 提到但未解释的主题
- 缺来源支撑的结论
- 已被新资料部分推翻但未修正的页面

输出要求：

- 先给一份 health report
- 修复前先告知，不要把“发现问题”和“自动改动”混成一步

当前可执行入口：

- `scripts/kb lint`
- 默认输出 `outputs/wiki-health-report-YYYY-MM-DD.md`

## 4. Update

目标：

- 把新证据合并进已有知识，而不是制造重复页面
- 保留仍正确的旧内容，只替换过时部分

核心原则：

- 优先更新已有话题页
- 不因为有新资料就重写整页
- 知识默认只增不减，但允许修正旧判断

最小流程：

1. 找到对应的已有主题页
2. 标出哪些内容仍然成立
3. 标出哪些内容已过时或被新资料修正
4. 只改动受影响部分
5. 补充来源、修订说明与版本痕迹
6. 更新 `wiki/log.md` 与必要的索引页

## How To Think About Confluence-Like Sources

如果上游是 Confluence，这个仓库的处理方式是：

- Confluence 原始页面进入 `raw/`
- 去重和精炼发生在 `wiki/`
- 查询时同时看原页面和已合成页
- 回答优先使用已合成页，原页面负责可点击回溯

也就是说，Confluence 更像原料仓，而不是直接被当成最终知识层。

## Common Mistakes

- ingest 时只是搬运原文，没有提炼结构
- query 时直接回原料重读，没有先用 wiki
- lint 时只找内容问题，不找断链、过期、孤儿页
- update 时新建一堆重复页，而不是更新已有页
- 发现新证据后静默覆盖旧判断，没有留下修订痕迹

## Rule of Thumb

可以把这四种模式压成一句话：

**Ingest 负责提炼，Query 负责复用，Lint 负责体检，Update 负责增量修订。**

## Source Trace

这页主要由以下页面收束而来：

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md)
- [README.md](/Users/ddz/Documents/exp/README.md)
- [how-to-route-knowledge-queries-in-this-repo.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-route-knowledge-queries-in-this-repo.md)
- [how-to-promote-outputs-into-frameworks-or-workflows.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md)

## Links

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md)
- [README.md](/Users/ddz/Documents/exp/README.md)
- [how-to-route-knowledge-queries-in-this-repo.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-route-knowledge-queries-in-this-repo.md)
- [how-to-promote-outputs-into-frameworks-or-workflows.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md)
