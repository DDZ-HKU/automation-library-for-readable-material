---
title: How to Promote Outputs into Frameworks or Workflows
updated: 2026-04-13
status: active
---

# Summary

`outputs/` 用来保存具体问题的答案、报告和阶段性成果，但不是所有高价值 output 都应永远停留在 `outputs/`。当一个 output 已经提炼出可迁移的判断模板时，应升格到 `wiki/notes/frameworks/`；当它已经形成可重复执行的步骤和协议时，应升格到 `wiki/notes/workflows/`。这页的作用，是定义升格边界和执行流程，避免知识库长期把稳定模式堆在 `outputs/` 里。

## Confirmed Understanding

- [[tacit-knowledge-layer]] / [../frameworks/tacit-knowledge-layer.md](../frameworks/tacit-knowledge-layer.md) 已确认，`wiki/notes/` 的职责不是重复摘要，而是沉淀可复用的思考方式、判断框架和应用方法。
- [[research-reading-and-decision-stack]] / [../frameworks/research-reading-and-decision-stack.md](../frameworks/research-reading-and-decision-stack.md) 已确认，新材料进入知识库后，需要判断它到底该更新哪一层。
- [[how-to-turn-paper-reading-into-research-decisions]] / [../frameworks/how-to-turn-paper-reading-into-research-decisions.md](../frameworks/how-to-turn-paper-reading-into-research-decisions.md) 已确认，知识库动作至少包括：更新 `concepts`、更新 `notes/frameworks`、更新 `notes/cases` 或保存到 `outputs/`。
- 当前仓库的 `outputs/` 已经承担了一部分“阶段性外显化”的作用，因此需要额外规则，决定哪些 output 应该进一步升格。

## Promotion Decision

### 什么时候只留在 `outputs/`

满足大部分以下特征时，通常只保留在 `outputs/`：

- 主要在回答一次具体问题
- 结论依赖当前上下文，迁移性弱
- 更像阶段 memo、简报或比较结果
- 即使有价值，也还没有稳定到足以变成长期规则

### 什么时候升格到 `wiki/notes/frameworks/`

满足大部分以下特征时，应优先升格到 `frameworks/`：

- 它教会了我们一种可迁移的判断方式
- 它能跨多个主题或多次任务复用
- 它回答的是“应该如何思考、判断、取舍”
- 它已经不只是面向当前问题，而是在压缩一类问题的分析模板

### 什么时候升格到 `wiki/notes/workflows/`

满足大部分以下特征时，应优先升格到 `workflows/`：

- 它定义了一条可重复执行的动作链
- 它回答的是“遇到这种情况应该按什么步骤做”
- 它包含明确的顺序、检查点或 handoff 规则
- 它会直接改变知识库 agent 的操作习惯或仓库协议

### 什么时候应更新 `wiki/concepts/`

如果 output 的真正价值在于修正了某个主题知识本身，而不是提炼出方法或流程，应优先更新 `concepts/`：

- 某个主题的新事实或新结构被确认
- 原有主题页的判断已被修正
- 变化发生在“知道什么”，而不是“怎么判断”或“怎么做”

## Decision Signals

判断一个 output 是否应升格时，优先看这 4 个信号：

1. 可迁移性
   - 它能不能在别的主题或别的任务里复用？
2. 可重复性
   - 它是不是已经形成稳定步骤，而不是一次性思路？
3. 协议影响
   - 它会不会改变 agent 以后该怎么读、怎么做、怎么停？
4. 知识层归属
   - 它真正改变的是 `concept`、`framework`、`workflow`，还是仅仅值得保留为 output？

## Quick Matrix

- 一次性问题答案 -> `outputs/`
- 可迁移判断模板 -> `wiki/notes/frameworks/`
- 可重复执行流程 -> `wiki/notes/workflows/`
- 主题知识本身变化 -> `wiki/concepts/`

如果一个 output 同时具备判断模板和执行步骤：

- 优先把“如何判断”沉淀为 `framework`
- 再把“如何执行”沉淀为 `workflow`

不要把两者混成一页，除非它们本来就不可分。

## Promotion Flow

当一个 output 看起来已经超过“一次性成果”时，按下面流程处理：

1. 先完成当前问题的回答，并把结果保存到 `outputs/`
2. 检查这个 output 的核心价值到底是：
   - 主题知识
   - 判断模板
   - 执行流程
   - 还是仅需保留为产物
3. 如果主要是判断模板，提炼到 `wiki/notes/frameworks/`
4. 如果主要是执行流程，提炼到 `wiki/notes/workflows/`
5. 如果主要是主题知识，更新 `wiki/concepts/`
6. 在新页或更新页中，显式回链到相关 `output`
7. 更新 `wiki/INDEX.md`
8. 追加 `wiki/log.md`

## How To Write the Promoted Page

### 升格为 framework 时

至少回答：

- 这类问题该怎么想
- 关键判断维度是什么
- 常见误判是什么
- 如何迁移到别的类似问题

### 升格为 workflow 时

至少回答：

- 这类情况该按什么顺序做
- 每一步的输入和输出是什么
- 哪些检查点是强制的
- 何时继续，何时停止，何时 handoff

## Common Mistakes

- 看到高价值 output 就机械地复制到 `notes/`
- 把一次性 memo 硬写成 framework
- 把判断规则和执行流程混成一块，导致后续难复用
- 明明应更新 `concepts/`，却只新增了一个 note
- 升格后忘记更新 `INDEX` 和 `log`

## Pending Inference

- 随着仓库继续增长，后续可能需要更显式的“升格队列”或 review 机制，而不只是靠单次判断决定是否升格。
- 如果 `outputs/` 数量继续增加，可能还需要增加“哪些 output 尚未升格但值得回看”的索引页。

## Links

- [[tacit-knowledge-layer]] / [../frameworks/tacit-knowledge-layer.md](../frameworks/tacit-knowledge-layer.md)
- [[research-reading-and-decision-stack]] / [../frameworks/research-reading-and-decision-stack.md](../frameworks/research-reading-and-decision-stack.md)
- [[how-to-turn-paper-reading-into-research-decisions]] / [../frameworks/how-to-turn-paper-reading-into-research-decisions.md](../frameworks/how-to-turn-paper-reading-into-research-decisions.md)
- [[how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases]] / [../frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](../frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)
