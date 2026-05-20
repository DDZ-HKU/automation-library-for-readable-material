---
title: How Agents Should Govern Links and Diffs in This Knowledge Base
updated: 2026-05-05
status: active
---

# Summary

在这个知识库里，增量维护的默认入口不是整页重读，而是先看聚焦后的 diff。对 agent 来说，`scripts/kb review-diff` 是所有知识库增量维护任务的硬性起手动作；只有当 diff 已不足以解释主题、证据或结构变化时，才升级为整页阅读。与此同时，页面页尾的链接区块不是兜底堆放区，而是需要按职责和预算治理的关系层。

## Why This Guide Exists

当前仓库的维护工作有一个明显风险：一旦 agent 在局部修订、断链修复、output 回灌、索引同步这些场景里默认整页重读，就会消耗过多上下文，并更容易顺手改动无关部分。另一边，如果 agent 看到有关系就不断往 `Links`、`Related Pages`、`Source Trace` 里追加链接，页面会迅速膨胀，最后既难读也难维护。

这页 guide 的目标，就是把这两个问题一起收束：

- 用 diff 约束 agent 如何观察增量改动
- 用预算约束 agent 如何落盘关系链接

## Hard Rule

只要任务属于知识库增量维护，agent 必须先运行：

```bash
scripts/kb review-diff
```

这里的“增量维护”至少包括：

- `update` 模式下的局部修订
- 断链修复
- output 回灌 wiki
- `wiki/INDEX.md` / `wiki/log.md` / `wiki/overview.md` 同步
- lint 后的定点修复
- 入口规则在 `README.md` / `AGENTS.md` 的增量收束

## Review-Diff Views

### Default View

默认执行：

```bash
scripts/kb review-diff
```

默认范围：

- `wiki/`
- `outputs/`
- `README.md`
- `AGENTS.md`

它的职责是让 agent 先看这轮知识维护真正触碰了哪些入口层和知识层文件。

### Index View

如果任务主要是入口同步，使用：

```bash
scripts/kb review-diff index
```

范围应聚焦：

- `wiki/INDEX.md`
- `wiki/log.md`
- `wiki/overview.md`
- `README.md`
- `AGENTS.md`

### Page View

如果任务明确只围绕单页维护，使用：

```bash
scripts/kb review-diff page <path>
```

`page` 视图默认只看该页面本身，不自动带上索引页、log、related outputs 或 notes。这样可以避免 agent 在单页修订里把视野过早扩张。

## When Agents Must Read the Full Page

即使已经先跑了 `review-diff`，下面这些情况仍必须升级为整页阅读：

- 首次理解一个主题
- 判断是否新建页、合并页、拆分页
- 处理冲突证据
- diff 已不足以解释这次关系变化
- 判断一个链接是否真的帮助理解，而不是只是“有关系”

也就是说，`review-diff` 是硬性起手动作，但不是整页阅读的替代品。

## Link Governance Rules

页尾默认保留三块：

- `Source Trace`
- `Related Pages`
- `Links`

它们的职责必须分开：

- `Source Trace` 只回答“这页判断从哪来”
- `Related Pages` 只回答“看完这页，下一步最值得联到哪几页”
- `Links` 只放少数导航性或功能性入口

不要把三块混成“把所有有关系的页面都挂上去”。

## Default Link Budgets

默认预算如下：

- `Source Trace`: `3-6`
- `Related Pages`: `3-5`
- `Links`: `2-4`

这些预算不是死板上限，而是默认收缩力。它们的作用是阻止 agent 把页尾写成全量邻接表。

## Valid Reasons to Exceed Budget

如果某一块超过默认预算，agent 必须能说明这是因为页面承担了额外职责，而不是因为“不想漏掉任何相关页”。

有效理由通常只有这些：

- 当前页本身是一个 hub page
- 当前页跨了两个以上主题线
- 当前页涉及 output promotion / partial promotion，需要显式保留上游和下游依赖
- 当前页是 workflow，需要同时保留规则页、入口页和脚本页

无效理由包括：

- “这些页面都有一点关系”
- “怕以后找不到”
- “先都挂上，后面再删”

## Shrink Order

当页尾过长时，默认按这个顺序删减：

1. 先删 `Links` 里泛化、弱帮助的导航入口
2. 再删 `Related Pages` 里非关键横向关系
3. `Source Trace` 最后删，优先保留直接证据，删除间接或重复上游

也就是说，页尾维护目标不是“尽量全”，而是“尽量有解释力”。

## Common Failure Modes

- 把 `review-diff` 当作首次理解主题的唯一入口
- 单页修订时顺手把无关页尾关系也扩写
- 在 `Source Trace` 里混入“相关推荐”
- 在 `Related Pages` 里堆全量相关页，而不是保留最关键几页
- 工作区很脏时不做聚焦 diff，直接整仓 `git diff`

## Rule of Thumb

可以把这页 guide 压成一句话：

**增量维护先看 `review-diff`，落盘关系按职责限量；如果 diff 已解释不了问题，再回整页。**

## Source Trace

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md)
- [README.md](/Users/ddz/Documents/exp/README.md)
- [how-to-run-ingest-query-lint-update-in-this-repo.md](how-to-run-ingest-query-lint-update-in-this-repo.md)
- [how-to-route-knowledge-queries-in-this-repo.md](how-to-route-knowledge-queries-in-this-repo.md)
- [how-to-manage-partially-promoted-outputs.md](how-to-manage-partially-promoted-outputs.md)

## Related Pages

- [[how-to-run-ingest-query-lint-update-in-this-repo]] / [how-to-run-ingest-query-lint-update-in-this-repo.md](how-to-run-ingest-query-lint-update-in-this-repo.md)
- [[how-to-route-knowledge-queries-in-this-repo]] / [how-to-route-knowledge-queries-in-this-repo.md](how-to-route-knowledge-queries-in-this-repo.md)
- [[how-to-manage-partially-promoted-outputs]] / [how-to-manage-partially-promoted-outputs.md](how-to-manage-partially-promoted-outputs.md)

## Links

- [../../../scripts/kb](/Users/ddz/Documents/exp/scripts/kb)
- [../../INDEX.md](../../INDEX.md)
