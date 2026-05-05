---
title: Workflow Index
updated: 2026-04-14
status: active
---

# Summary

这个索引页不是重复列出所有 workflow，而是给当前仓库提供一张“工作流使用地图”：遇到知识查询、产物升格、自主运行或规则治理问题时，应该先看哪一页。它的目标是减少 workflow 页自身的分散感，让后续使用者不必先扫完整个目录。

## By Use Case

### 查询与回答

- [[how-to-route-knowledge-queries-in-this-repo]] / [how-to-route-knowledge-queries-in-this-repo.md](how-to-route-knowledge-queries-in-this-repo.md)
  - 何时先看 `concepts`、`notes`、`outputs` 或 `raw`
- [[how-to-run-ingest-query-lint-update-in-this-repo]] / [how-to-run-ingest-query-lint-update-in-this-repo.md](how-to-run-ingest-query-lint-update-in-this-repo.md)
  - 统一定义 `Ingest / Query / Lint / Update` 四种核心运行模式

### 产物沉淀与升格

- [[how-to-promote-outputs-into-frameworks-or-workflows]] / [how-to-promote-outputs-into-frameworks-or-workflows.md](how-to-promote-outputs-into-frameworks-or-workflows.md)
  - 何时把结果留在 `outputs`，何时升格到 wiki
- [[how-to-manage-partially-promoted-outputs]] / [how-to-manage-partially-promoted-outputs.md](how-to-manage-partially-promoted-outputs.md)
  - 当 output 已部分回灌到 wiki 后，如何继续管理

### 研究推进

- [[how-to-write-a-stage-research-decision-memo]] / [how-to-write-a-stage-research-decision-memo.md](how-to-write-a-stage-research-decision-memo.md)
  - 如何为一个主题线写阶段研究决策 memo

### 技能与协议验证

- [[how-to-validate-knowledge-base-agent-skills]] / [how-to-validate-knowledge-base-agent-skills.md](how-to-validate-knowledge-base-agent-skills.md)
  - 如何验证知识库 skills 是否真的可用

### 健康检查

- [[how-to-run-ingest-query-lint-update-in-this-repo]] / [how-to-run-ingest-query-lint-update-in-this-repo.md](how-to-run-ingest-query-lint-update-in-this-repo.md)
  - 当前 `Lint` 模式的执行入口是 `scripts/kb lint`

### 运行协议与治理

- [[how-to-apply-ops-protocol-outside-autonomous-runs]] / [how-to-apply-ops-protocol-outside-autonomous-runs.md](how-to-apply-ops-protocol-outside-autonomous-runs.md)
  - 哪些 `ops` 规则只适用于 autonomous run，哪些应外溢到普通工作
- [[how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol]] / [how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md](how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md)
  - 如何给当前仓库里的规则对象归类

### 资料预处理

- [[pdf-to-markdown-preprocessing]] / [pdf-to-markdown-preprocessing.md](pdf-to-markdown-preprocessing.md)
  - 如何把 PDF 先转成 Markdown 再进入 ingest

## Short Reading Paths

### 如果你只是要回答一个问题

1. [[how-to-route-knowledge-queries-in-this-repo]] / [how-to-route-knowledge-queries-in-this-repo.md](how-to-route-knowledge-queries-in-this-repo.md)
2. 如需确认当前模式边界，再看 [[how-to-run-ingest-query-lint-update-in-this-repo]] / [how-to-run-ingest-query-lint-update-in-this-repo.md](how-to-run-ingest-query-lint-update-in-this-repo.md)

### 如果你要统一强化仓库的四种知识操作

1. [[how-to-run-ingest-query-lint-update-in-this-repo]] / [how-to-run-ingest-query-lint-update-in-this-repo.md](how-to-run-ingest-query-lint-update-in-this-repo.md)
2. 再按需要跳到具体 query routing 或 output promotion guide

### 如果你刚写完一个 output，想判断要不要回灌

1. [[how-to-promote-outputs-into-frameworks-or-workflows]] / [how-to-promote-outputs-into-frameworks-or-workflows.md](how-to-promote-outputs-into-frameworks-or-workflows.md)
2. 如已部分升格，再看 [[how-to-manage-partially-promoted-outputs]] / [how-to-manage-partially-promoted-outputs.md](how-to-manage-partially-promoted-outputs.md)

### 如果你要连续推进一个主题线

1. [[how-to-write-a-stage-research-decision-memo]] / [how-to-write-a-stage-research-decision-memo.md](how-to-write-a-stage-research-decision-memo.md)

### 如果你要判断一条新规则该落在哪

1. [[how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol]] / [how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md](how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md)

### 如果你要做长时运行或借用 `ops` 协议

1. [[how-to-apply-ops-protocol-outside-autonomous-runs]] / [how-to-apply-ops-protocol-outside-autonomous-runs.md](how-to-apply-ops-protocol-outside-autonomous-runs.md)
2. 再结合 `ops/runbook.md` 和 `ops/workboard.md`

## How To Maintain This Index

- 新增 workflow 后，应至少在一个 use case 分组里挂上它
- 如果某类问题已经有两个以上 workflow，优先补一个 short reading path
- 不要把这个索引页写成重复摘要；它只负责导航

## Links

- [../frameworks/tacit-knowledge-layer.md](../frameworks/tacit-knowledge-layer.md)
- [../../INDEX.md](../../INDEX.md)
