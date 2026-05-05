# 隐性约定盘点

日期：2026-04-14

## 这份 audit 在做什么

这份 audit 不是新增规则，而是盘点当前仓库里已经存在、但仍分散在不同页面和惯例里的约定。

目标是把它们分成四类：

- `已显式写明`
- `仍属隐性但已分散存在`
- `边界不清或容易冲突`
- `最值得优先升格成 guide`

## 盘点范围

本次盘点覆盖四类约定：

1. 知识查询约定
2. 自主运行约定
3. 沉淀与升格约定
4. 工具与治理约定

主要依据来自：

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md)
- [README.md](/Users/ddz/Documents/exp/README.md)
- [ops/runbook.md](/Users/ddz/Documents/exp/ops/runbook.md)
- [ops/workboard.md](/Users/ddz/Documents/exp/ops/workboard.md)
- [ops/handoff.md](/Users/ddz/Documents/exp/ops/handoff.md)
- [how-to-promote-outputs-into-frameworks-or-workflows.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md)
- [how-to-write-a-stage-research-decision-memo.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-write-a-stage-research-decision-memo.md)
- [how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)
- [harness-engineering-implications-for-this-knowledge-base-2026-04-13.md](/Users/ddz/Documents/exp/outputs/harness-engineering-implications-for-this-knowledge-base-2026-04-13.md)

## 一、知识查询约定

### 已显式写明

- 非平凡问题先读 `wiki/INDEX.md`
- 优先基于 `wiki/` 回答，不足时再回 `raw/`
- 需要高层理解、判断或应用时，优先查 `wiki/notes/`
- query 结果有长期价值时，应保存到 `outputs/`

这些规则已经清楚分布在：

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md)
- [.codex/skills/kb-wiki-first/SKILL.md](/Users/ddz/Documents/exp/.codex/skills/kb-wiki-first/SKILL.md)

### 仍属隐性但已分散存在

- 什么时候先看 `notes/frameworks`，什么时候先看 `notes/cases`
- 什么情况下应优先查已有 `outputs/` 而不是概念页
- 在多条相关知识线同时存在时，应如何确定“主入口页”

这些现在已经能从现有 pages 推出来，但还没有一页明确写成查询 guide。

### 边界不清

- “wiki 不足” 到底是资料不足，还是只是缺更合适的 tacit page
- “优先基于 wiki 回答” 与 “先看 outputs 找现成可复用回答” 之间的优先级还不够显式

### 最值得优先升格

- 一页 `how-to-route-knowledge-queries-in-this-repo`

它应明确：

- 先看 `concepts` 还是 `notes`
- 什么问题先看 `outputs`
- 何时回 `raw`
- 何时只做回答，何时同步沉淀

## 二、自主运行约定

### 已显式写明

- 启动顺序：`charter -> workboard -> handoff -> runbook`
- 默认执行循环：选任务、执行、验证、checkpoint、继续或 handoff
- 必跑脚本：
  - `ops-phase-status`
  - `ops-check-handoff-readiness`
  - `ops-verify-continuation`
- 只有 `phase-complete`、`decision-required`、`blocked` 才是有效停止条件
- handoff 前必须验证

这些规则已经非常清楚地写在：

- [ops/runbook.md](/Users/ddz/Documents/exp/ops/runbook.md)
- [agent/skills/kb-autonomous-run/SKILL.md](/Users/ddz/Documents/exp/agent/skills/kb-autonomous-run/SKILL.md)

### 仍属隐性但已分散存在

- 什么算“meaningful execution batch”
- 什么情况下应该写 forced early handoff，而不是继续试修
- verification 失败后，下一轮应优先修哪里，仍偏经验性

### 边界不清

- `ops/` 协议适用于自主运行，但哪些部分也适用于普通 query / ingest 任务，还没有显式写明
- “自然交接点” 的定义已经清楚，但“非 phase 工作”如何 handoff 还没有统一模板

### 最值得优先升格

- 一页 `how-to-apply-ops-protocol-outside-autonomous-runs`

它应回答：

- 普通 ingest / synthesis 任务是否也要套用部分 runbook 规则
- 小型工作什么时候也应写 handoff

## 三、沉淀与升格约定

### 已显式写明

- query 有长期价值时先写 `outputs/`
- 判断模板升格到 `frameworks`
- 执行流程升格到 `workflows`
- 主题知识变化更新 `concepts`
- 主题型 tacit 解读进入 `cases`

这些规则已经系统化写在：

- [how-to-promote-outputs-into-frameworks-or-workflows.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md)

### 仍属隐性但已分散存在

- 哪类 `outputs/` 应被视作“上游草稿”，值得后续主动巡检
- “部分升格” 这种中间状态如何长期管理
- 哪些 output 需要双向 `Source Trace`，哪些不需要

### 边界不清

- `framework` 与 `case` 的边界在一些主题型长文上仍可能模糊
- “保留 output” 与 “部分升格” 的标准现在主要靠人工判断

### 最值得优先升格

- 一页 `how-to-manage-partially-promoted-outputs`

它应明确：

- 何时补 `Source Trace`
- 何时需要双向回链
- 何时把部分升格对象进一步收束掉

## 四、工具与治理约定

### 已显式写明

- 仓库已经分成：
  - `raw -> wiki -> outputs` 内容流
  - `atomic -> facade -> planning -> governance` 工具流
- `scripts/` 承担 facade
- `agent/skills/` 承担 route / planning
- `ops/` 承担 governance

这些规则已经清楚写在：

- [how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)
- [harness-engineering-implications-for-this-knowledge-base-2026-04-13.md](/Users/ddz/Documents/exp/outputs/harness-engineering-implications-for-this-knowledge-base-2026-04-13.md)

### 仍属隐性但已分散存在

- 当前哪些 repo 约定已经算 `feedforward guides`
- 当前哪些 scripts / checks 已经算 `feedback sensors`
- 哪些 scripts 只是便利工具，哪些已经是 protocol checkpoints

### 边界不清

- `scripts/kb` 等 facade 的元信息仍不够显式
- `agent/maps/*` 和普通文档之间的角色边界还没完全写明
- `ops/` 作为 deterministic infrastructure 的说明还散落在多页

### 最值得优先升格

- 一页 `how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol`

它应把当前仓库里的规则对象分成：

- guide
- sensor
- facade
- protocol

这样后续新增规则时就不必再凭感觉归类。

## 五、最明显的冲突风险

当前没有严重冲突，但有 3 处容易随着仓库增长变模糊：

1. `query` 时先看 `notes` 还是先看 `outputs`
2. `framework`、`case` 与“部分升格 output”之间的边界
3. `ops` 协议是只限 autonomous run，还是已经部分成为全仓默认规范

## 六、优先级建议

如果要把这次 audit 转成真正的 guide 落地，建议按这个顺序推进：

1. `知识查询 guide`
2. `部分升格 output 管理 guide`
3. `规则分类 guide`
4. `ops 协议外溢 guide`

原因是：

- 第一项最直接影响日常 query 质量
- 第二项最直接影响知识库长期可维护性
- 第三项最直接影响后续 harness 扩张时不混层
- 第四项更偏高级治理，可放后

## 一句话总结

当前仓库的隐性约定已经不少，但并不是“完全没规则”，而是：

**规则已经存在，只是还分散在 query、ops、promotion、tool-governance 几条线里。下一步最该做的，不是再发明新规则，而是把这些已存在规则重新编排成更少、更清楚、更可机器读取的 guides。**
