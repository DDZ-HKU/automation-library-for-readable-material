---
title: How to Read a Tool Paper for System Construction
updated: 2026-04-13
status: active
---

# Summary

读 tool 论文时，最容易犯的错误，不是没记住系统组件名，而是把“会用工具”“会造工具”“会组织工具库”这些口号，当成已经解释了系统是怎么搭起来的。真正有用的读法，不是只问它解决了什么抽象问题，而是进一步问：这个系统的部件是什么，部件之间怎样分工，哪一层是真正的瓶颈，哪些部分属于可迁移的系统结构。

## Confirmed Understanding

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md) 已确认，tool 相关工作至少可分成 `tool use`、`tool making`、`tool library`，并外延到 `evaluation` 与 `serving`。
- [[tool-paper-comparison-matrix]] / [tool-paper-comparison-matrix.md](tool-paper-comparison-matrix.md) 已确认，比较 tool 论文时，至少要按六个维度拆，而不能混成同一类。
- [[how-to-think-about-evaluation-and-serving-in-tool-agent-systems]] / [how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md](how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md) 已确认，`evaluation` 与 `serving` 不是收尾细节，而是系统能力本身的一部分。
- `outputs/how-the-tool-papers-actually-implement-their-systems-2026-04-13.md` 已展示，ToolLLM、CREATOR、LATM、ToolLibGen 与 API synthesis 并不是同一个实现模板，而是五种不同的系统构造方式。

## Tacit Interpretation

- 对 tool 论文来说，只看“核心 idea”远远不够，因为它们往往真正贡献的是系统分工，而不是单个技巧。
- 你真正想学的，不是论文里列了几个模块，而是：
  - 哪些模块必须一起出现
  - 哪些模块在运行时分工
  - 哪些模块定义了系统瓶颈
- 因此，读 tool 论文时，系统实现层和模型机制层一样重要。

## How To Read

建议按下面顺序读，而不是只从 abstract 滑到实验结果：

1. 先判断这篇论文在系统里主攻哪一层
2. 再列出它的核心部件
3. 再看这些部件如何分工
4. 再看瓶颈被放在哪一层解决
5. 最后才判断哪些实现结构值得迁移

### 1. 先判断主攻层

先问：

- 它主要在解决 `tool use`、`tool making`、`tool library`，还是 `api synthesis`？
- 它的重点在：
  - 检索
  - 规划
  - 执行
  - 评估
  - serving

如果这一步不做，后面很容易把不同论文错当成同类竞争。

### 2. 列出核心部件

不要只写“提出了一个框架”，而要把系统拆成部件清单。

例如：

- ToolLLM：
  - `ToolBench`
  - `ToolLLaMA`
  - `API retriever`
  - `DFSDT`
  - `ToolEval`
- CREATOR：
  - `Creation`
  - `Decision`
  - `Execution`
  - `Rectification`
- LATM：
  - `tool maker`
  - `tool user`
  - `functional cache`

如果你列不出部件，通常说明你还停留在论文宣传语里。

### 3. 看部件如何分工

继续问：

- 这些部件分别负责什么？
- 哪些是离线构建，哪些是运行时组件？
- 哪些是高成本前置步骤，哪些是低成本重复执行步骤？

这一步很关键，因为 tool 论文的长期价值，经常来自分工方式，而不是单点算法。

### 4. 看瓶颈放在哪一层解决

接着问：

- 这篇论文真正承认的系统瓶颈是什么？
- 它把瓶颈放在：
  - 数据构造
  - 检索
  - 推理结构
  - 评估
  - 成本/服务分工
  - 资产治理
  的哪一层来解决？

如果一篇论文没有说明瓶颈落点，往往很难判断它为什么要长成现在这套系统。

### 5. 判断可迁移的系统结构

最后问：

- 哪些组件组合是必须一起带走的？
- 哪些只是特定 benchmark 下的实现细节？
- 这篇论文真正可迁移的，是一个模块，还是一套分工结构？

## Reading Questions

读每篇 tool 论文时，至少回答下面这些问题：

1. 这篇论文主攻哪一层问题？
2. 它的系统最小闭环由哪些部件组成？
3. 哪些部件是训练/构建期的，哪些是运行时的？
4. 它真正把瓶颈放在哪一层解决？
5. `evaluation` 和 `serving` 在系统里处于什么位置？
6. 哪部分实现结构最值得迁移到别的项目？

## How To Judge Transfer Value

对 tool 论文，迁移价值通常不在单个 prompt，而在这些层面：

- 分工结构
  - 例如 maker/user split
- 系统闭环
  - 例如 retriever + planner + evaluator
- 治理结构
  - 例如 clustering + aggregation + review
- 运行结构
  - 例如 functional cache、审批、trace、handoff

如果一篇论文脱离原 benchmark 后还留下了这些结构，它的长期价值通常就不低。

## How To Apply

### 读论文时

- 除了记结论，再补一张“系统部件表”。
- 记录：
  - 组件
  - 分工
  - 瓶颈层
  - evaluation
  - serving

### 做项目映射时

- 不要急着把论文翻译成“加一个脚本”或“写一个 agent”。
- 先判断你真正要借鉴的是：
  - 一个部件
  - 一种分工
  - 还是一整套闭环

### 做知识库整理时

- 如果一份 output 已经把论文的系统构造方式讲清楚，它通常不应只留在 `outputs/`。
- 更合理的做法是把它进一步提升成 `wiki/notes/frameworks/`，供后续反复复用。

## Common Mistakes

- 把系统论文当成纯模型论文读
- 只记模块名，不记模块分工
- 只记主算法，不记 evaluator 或 serving 结构
- 把 benchmark 结果误判成系统结构本身

## What Is Still Missing

- 当前知识库还没有单独整理不同 retriever 设计的比较框架。
- 当前知识库还没有单独整理 tool paper 中“训练期组件”和“运行期组件”的通用拆分法。
- 关于 API synthesis 与 tool creation 的实现边界，仍需要更多材料来验证。

## Source Trace

这页主要由以下已有产物与页面提炼而来：

- [../../../outputs/how-the-tool-papers-actually-implement-their-systems-2026-04-13.md](../../../outputs/how-the-tool-papers-actually-implement-their-systems-2026-04-13.md)
- [tool-paper-comparison-matrix.md](tool-paper-comparison-matrix.md)
- [how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md](how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md)

## Links

- [[tool-paper-comparison-matrix]] / [tool-paper-comparison-matrix.md](tool-paper-comparison-matrix.md)
- [[how-to-think-about-evaluation-and-serving-in-tool-agent-systems]] / [how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md](how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md)
- [[research-reading-and-decision-stack]] / [research-reading-and-decision-stack.md](research-reading-and-decision-stack.md)
- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md)
