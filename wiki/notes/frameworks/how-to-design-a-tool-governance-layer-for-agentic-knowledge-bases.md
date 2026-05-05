---
title: How to Design a Tool Governance Layer for Agentic Knowledge Bases
updated: 2026-04-13
status: active
---

# Summary

当知识库开始引入 `scripts/`、`agent/skills/` 和 `ops/` 这类 agent 工程部件后，问题就不再只是“知识怎么提取”，而变成“知识系统如何把工具能力组织成稳定工作流”。最稳的设计不是把所有原子 CLI 直接暴露给 agent，而是把知识库的工具层显式分成：原语层、任务门面层、规划层和治理层。

## Confirmed Understanding

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md) 已确认，tool use 不是单次调用，而是检索、选择、执行、反馈和评估的完整链条。
- [[how-to-aggregate-atomic-cli-commands-for-agents]] / [how-to-aggregate-atomic-cli-commands-for-agents.md](how-to-aggregate-atomic-cli-commands-for-agents.md) 已确认，原子 CLI 如果长期作为主工作流，会把成本压到检索、排序和误用上。
- [[how-agents-should-plan-and-improve-atomic-cli-usage]] / [how-agents-should-plan-and-improve-atomic-cli-usage.md](how-agents-should-plan-and-improve-atomic-cli-usage.md) 已确认，最稳的演化路线是 `atomic call -> task facade -> search-based planning -> maker-user split -> library aggregation`。
- 当前仓库里已经存在这几层的最小对应物：
  - 原语层：`rg`、`sed`、`git status`、`pytest`
  - 任务门面层：`scripts/kb`、`scripts/pdf-to-md`
  - 规划层：`kb-route`、`kb-teach`、`kb-autonomous-run`
  - 治理层：`ops/runbook.md`、`ops/workboard.md`、`ops/handoff.md`

## Tacit Interpretation

- 对知识库来说，`scripts/` 不是附属小工具，而是把“知识提取动作”压缩成可复用接口的中层。
- `agent/skills/` 也不只是 prompt 片段，它们承担的是“如何检索、如何选择页面、何时沉淀”的规划职责。
- `ops/` 不只是流程文档，而是知识库 agent 的停止条件、验证边界和 handoff 规则，也就是治理层。
- 因此，一个成熟的 agentic knowledge base，不能只维护 `raw -> wiki -> outputs` 的内容流，还要维护一条与之平行的工具治理流：
  - 哪些原子动作允许直接暴露
  - 哪些高频流程必须提升成 facade
  - 哪些判断交给 skill 路由
  - 哪些停止和验证规则必须由 runbook 固化

## Explicit Knowledge vs Interpretation

### 已确认的显性知识

- 这个仓库已经不是纯静态 wiki，而是带有 repo-local tooling、repo-local skills 和 autonomous ops protocol 的知识库。
- 当前知识任务已默认采用 `wiki -> relevant notes/outputs -> raw` 的 `wiki-first` 路由。
- 当前知识库已经通过 `scripts/kb` 把部分高频检索动作从原子 CLI 提升成了 facade。

### 默会知识解读

- 这说明当前仓库已经进入“工具治理”问题域，而不只是“资料整理”问题域。
- 以后再扩张能力时，真正该优化的重点不会是“再多几个脚本”，而是：
  - 检索歧义是否下降
  - 路由是否更稳
  - 验证与停止条件是否更清楚
  - outputs 中的高价值模式是否被及时提升为 framework 或 workflow

### 待验证的推断

- 未来如果 `scripts/` 和 `agent/skills/` 数量继续增长，当前仓库很可能需要显式的工具索引或元数据层，而不仅是靠文件名和 `INDEX.md`。
- 当前 `scripts/kb related` 的发现能力偏弱，后续可能需要更强的关系提取或显式 backlink 约定。

## Layered Design

### 1. Atomic Layer

保留通用原语，但不让它们承担主流程语义。

当前对应：

- shell 原语：`rg`、`sed`、`ls`
- git 原语：`git status`
- verification 原语：`pytest`

设计要求：

- 标清哪些是只读、可写、高风险
- 默认把它们视为底层保底能力，而不是首选入口

### 2. Facade Layer

把高频且顺序稳定的知识库动作升格成可复用入口。

当前对应：

- `scripts/kb`
- `scripts/pdf-to-md`

设计要求：

- 输入边界清晰
- 输出格式稳定
- 任务语义高于底层命令细节

### 3. Planning Layer

把“如何找页、如何讲解、何时回 raw、何时沉淀 output”这类判断交给 skills 和 playbooks。

当前对应：

- `kb-wiki-first`
- `kb-route`
- `kb-ask`
- `kb-teach`
- `kb-explain-page`
- `kb-autonomous-run`

设计要求：

- route 明确
- 页面读取顺序明确
- 显性知识、默会知识、推断要分开

### 4. Governance Layer

把继续执行、验证完成、何时 handoff 这些规则从 agent 的临场判断里拿出来，变成仓库协议。

当前对应：

- `ops/runbook.md`
- `ops/workboard.md`
- `ops/handoff.md`
- continuation scripts

设计要求：

- stop condition 可检查
- verification 在 handoff 前强制发生
- 当前 phase 与下一 phase 的边界清楚

## Mapping to This Repository

这份设计对当前知识库的直接映射可以压成四句：

1. `raw -> wiki -> outputs` 是内容流。
2. `atomic -> facade -> planning -> governance` 是工具流。
3. `scripts/` 负责把高频动作从原子命令提升成任务入口。
4. `agent/skills/` 与 `ops/` 负责把这些任务入口接成可持续运行的知识库协议。

按这个视角看：

- `scripts/kb` 解决的是知识检索层的 facade 问题。
- `kb-route` / `kb-teach` 解决的是知识任务的 planning 问题。
- `kb-autonomous-run` 加 `ops/runbook.md` 解决的是“什么时候继续跑、什么时候该停”的 governance 问题。

## How To Apply

如果以后要更新这个知识库的设计，优先按下面顺序判断：

1. 这是新的底层原语，还是重复出现的任务？
2. 如果是重复任务，是否该先提升成 `scripts/` facade？
3. 如果 facade 已经存在，agent 仍容易走错，是否该更新 `agent/skills/` 的路由与读取顺序？
4. 如果 agent 会在完成、验证、停机上反复失误，是否该更新 `ops/` 协议而不是继续补 prompt？
5. 如果一个 output 提炼出了长期稳定的判断模板，是否该提升到 `wiki/notes/frameworks/` 或 `wiki/notes/workflows/`？

## What Is Still Missing

- 还没有一页专门定义“何时把 output 升格为 framework，何时升格为 workflow”。
- 还没有给 repo-local tools 建立统一元信息层，例如用途、输入、输出、副作用和风险级别。
- 当前知识库对工具治理的观察还主要来自 tool 论文分支，后续需要更多真实仓库演化案例来验证。

## Source Trace

这页的主要上游 output 包括：

- [../../../outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md](../../../outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md)
- [../../../outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md](../../../outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md)

## Links

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md)
- [[how-to-aggregate-atomic-cli-commands-for-agents]] / [how-to-aggregate-atomic-cli-commands-for-agents.md](how-to-aggregate-atomic-cli-commands-for-agents.md)
- [[how-agents-should-plan-and-improve-atomic-cli-usage]] / [how-agents-should-plan-and-improve-atomic-cli-usage.md](how-agents-should-plan-and-improve-atomic-cli-usage.md)
- [[tool-use-tool-making-tool-library-branch]] / [../cases/tool-use-tool-making-tool-library-branch.md](../cases/tool-use-tool-making-tool-library-branch.md)
- [../../../outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md](../../../outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md)
- [../../../outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md](../../../outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md)
