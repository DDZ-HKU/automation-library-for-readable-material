---
title: How to Classify Repo Rules as Guides, Sensors, Facades, or Protocol
updated: 2026-04-14
status: active
---

# Summary

随着这个仓库逐步从静态知识库长成 agent system，规则对象已经不再只有“文档”一种形态。现在至少同时存在四类不同对象：`guides`、`sensors`、`facades`、`protocol`。如果不把它们区分开，后续新增规则时就会混层：本该写成 skill 的东西被塞进文档，本该做成脚本检查的东西被写成说明文字，本该是运行协议的东西被误当成普通知识页。

## Confirmed Understanding

- [how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md) 已确认，当前仓库已经分成：
  - `atomic`
  - `facade`
  - `planning`
  - `governance`
- [how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md) 已确认，agent harness 中至少要区分：
  - `feedforward guides`
  - `feedback sensors`
- [harness-engineering-implications-for-this-knowledge-base-2026-04-13.md](/Users/ddz/Documents/exp/outputs/harness-engineering-implications-for-this-knowledge-base-2026-04-13.md) 已确认，当前仓库已经可以按：
  - knowledge layer
  - feedforward layer
  - feedback layer
  - long-running control layer
  来理解。

## The Four Classes

### 1. Guide

定义：

- 主要作用是事前引导 agent
- 说明“应该怎么理解、怎么进入、怎么选择”
- 不直接执行，也不直接判定结果

典型对象：

- `AGENTS.md`
- `agent/skills/*`
- `agent/maps/*`
- 某些 `wiki/notes/frameworks/*`
- 某些 `wiki/notes/workflows/*`

它主要回答：

- 先读什么
- 按什么顺序做
- 遇到这种问题该怎么判断

### 2. Sensor

定义：

- 主要作用是事后检测或中途检查
- 用来回答“当前做得对不对”
- 可以是 deterministic，也可以是 inferential

典型对象：

- verification commands in `ops/workboard.md`
- `scripts/ops-check-handoff-readiness`
- `scripts/ops-verify-continuation`
- review / audit outputs

它主要回答：

- 这轮工作是否通过
- 是否能继续
- 是否能 handoff

### 3. Facade

定义：

- 把多个底层动作压成一个高语义任务入口
- 主要解决检索歧义和重复组合问题

典型对象：

- `scripts/kb`
- `scripts/pdf-to-md`
- 其他 task-oriented scripts

它主要回答：

- 这个任务该用哪个入口
- 能不能不用每次手工拼原子命令

### 4. Protocol

定义：

- 规定运行边界、stop condition、handoff 规则和角色分工
- 不是单步任务入口，而是整个 run 的约束结构

典型对象：

- `ops/runbook.md`
- `ops/workboard.md`
- `ops/handoff.md`
- `kb-autonomous-run`

它主要回答：

- 什么时候开始
- 什么时候继续
- 什么时候必须验证
- 什么时候允许停

## How To Classify

判断一个规则对象属于哪一类，优先问这 4 个问题：

1. 它主要在事前引导，还是事后检查？
2. 它是在定义单个任务入口，还是在定义整段运行协议？
3. 它是否把多个底层动作压成一个任务接口？
4. 它是否决定 stop / continue / handoff 这种运行边界？

## Quick Decision Rules

- 如果主要在事前引导 -> `guide`
- 如果主要在事后检查 -> `sensor`
- 如果主要把底层动作压成任务入口 -> `facade`
- 如果主要定义运行边界与交接规则 -> `protocol`

## How To Apply in This Repo

### 现有对象的推荐归类

#### Guides

- `AGENTS.md`
- `.codex/skills/kb-wiki-first/SKILL.md`
- `agent/skills/kb-route/SKILL.md`
- `wiki/notes/frameworks/*`
- 多数查询 / 沉淀 / 研究决策相关 workflow

#### Sensors

- `scripts/ops-check-handoff-readiness`
- `scripts/ops-verify-continuation`
- workboard 中的 verification method
- 各类 audit / test report / review 产物

#### Facades

- `scripts/kb`
- `scripts/pdf-to-md`

#### Protocols

- `ops/runbook.md`
- `ops/workboard.md`
- `ops/handoff.md`
- `kb-autonomous-run`

## Common Misclassifications

### 把 protocol 当 guide

比如：

- 把 stop condition 写成一页解释文字
- 却没有进入 `ops/` 协议或脚本检查

### 把 sensor 当 guide

比如：

- 明明需要一个可检查的 gate
- 却只写成“完成前最好验证一下”

### 把 facade 当普通脚本

比如：

- 明明已经是高频任务入口
- 但没有明确输入输出边界和任务语义

### 把 guide 当知识页

比如：

- 某些实际上在规定 agent 行为的内容
- 被埋在普通解释页里，导致 agent 不会稳定执行

## When a Rule Needs Promotion

如果某条规则当前只是隐性约定，但已经反复影响仓库运行，应优先问：

- 它该升格成 `guide` 还是 `protocol`？
- 它需要解释文字，还是需要可执行检查？

一个实用规则是：

- 如果目标是“让 agent 更容易做对” -> 更偏 `guide`
- 如果目标是“防止 agent 在错误状态继续跑” -> 更偏 `sensor` 或 `protocol`

## Minimal Workflow

1. 发现一个新规则或习惯
2. 先判断它是在引导、检测、聚合，还是约束运行边界
3. 把它归到 `guide / sensor / facade / protocol`
4. 再决定它应进入：
   - 文档
   - skill
   - script
   - `ops/`

## Source Trace

这页主要由以下材料收束而来：

- [how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)
- [how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md)
- [implicit-conventions-audit-2026-04-14.md](/Users/ddz/Documents/exp/outputs/implicit-conventions-audit-2026-04-14.md)

## Links

- [how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)
- [how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md)
- [implicit-conventions-audit-2026-04-14.md](/Users/ddz/Documents/exp/outputs/implicit-conventions-audit-2026-04-14.md)
