# Tool 论文结构化对照表

日期：2026-04-13

## 范围

当前纳入对照的 6 篇与 tool 相关材料：

1. `ToolLLM`
2. `LATM`
3. `CREATOR`
4. `ToolLibGen`
5. `API Synthesis Using LLMs`
6. `Agent/Harness 官方实践资料`

其中前 5 篇是本地论文材料，第 6 项是你前面让我整理 agent/harness 设计时使用并沉淀的官方实践层。

## 结构化矩阵

| 材料 | tool use | tool making | tool library | api synthesis | evaluation | serving |
|---|---|---|---|---|---|---|
| ToolLLM | 强。核心就是让开源 LLM 学会使用大量真实 API。 | 中。不是直接造工具，但通过 ToolBench 数据构造间接支持能力生成。 | 弱。重点不在库治理。 | 弱。不是综合新 API 实现。 | 很强。ToolEval 是论文核心组件之一。 | 中。涉及 API retriever 与完整 tool-use pipeline，但不是成本/服务主问题。 |
| LATM | 中。tool user 是系统的一半。 | 很强。核心就是让 LLM 充当 tool maker。 | 中。通过 reusable tools 与 functional cache 开始触及工具资产管理。 | 弱。不是传统 API synthesis。 | 中。通过任务效果验证 tool maker/user 分工是否成立。 | 很强。cost-performance tradeoff 与 functional cache 是核心卖点。 |
| CREATOR | 中。decision/execution 阶段包含 tool use。 | 很强。核心是 tool creation。 | 弱到中。强调工具生成与修正，但还没进入大规模库组织。 | 中。更接近“按问题创建工具”，但不是组件库驱动的 API synthesis。 | 中。通过 MATH、TabMWP、Creation Challenge 验证框架有效性。 | 弱。主要不是 serving/cost 论文。 |
| ToolLibGen | 中。最终仍用于 tool-augmented reasoning。 | 中。承认 question-specific tool creation 是前提，但不是主问题。 | 很强。核心就是 clustering、aggregation、structured library。 | 弱。不是直接综合 API 实现。 | 中。重点是 retrieval accuracy 和 reasoning performance。 | 中。更偏系统资产管理，而不是在线 serving 成本。 |
| API Synthesis Using LLMs | 弱。不是 agent-style tool use。 | 中。会生成 API 实现，但更像 synthesis，不是 agent 工具创造闭环。 | 弱。不是库组织论文。 | 很强。核心就是 component/API synthesis。 | 中。重点看 compile/pass/readability 等评估。 | 弱。不是 serving 架构。 |
| Agent/Harness 官方实践资料 | 中到强。强调 agent 如何选择和调用工具。 | 弱。不是专门研究 tool creation。 | 中。强调工具边界、schema、治理，但不是 ToolLibGen 式库聚合。 | 弱。不是 API synthesis 研究。 | 很强。eval-driven development、trace grader、结果评估是核心。 | 很强。run loop、审批、状态、环境、成本和控制都属于主问题。 |

## 一眼判断

如果把这 6 项放到一条更抽象的谱系里，可以这样理解：

- `ToolLLM`：先解决“会不会用”
- `CREATOR` / `LATM`：再解决“会不会造”
- `ToolLibGen`：再解决“造多了怎么管”
- `API Synthesis Using LLMs`：平行旁支，解决“能不能直接综合实现”
- `Agent/Harness 官方实践资料`：系统底座，解决“整个工具使用/创建/治理流程怎么稳定跑起来”

## 最值得保留的判断

### 1. `tool use` 和 `tool making` 不是一回事

- ToolLLM 偏 use
- CREATOR / LATM 偏 make

不要把它们混成“都会调函数”。

### 2. `tool library` 是独立层，不是附属优化

ToolLibGen 说明：当工具规模化后，真正的瓶颈会从 creation 上移到 organization / retrieval。

### 3. `api synthesis` 是旁支，不应硬塞进主线

`API Synthesis Using LLMs` 更接近 program synthesis，虽然和 tool creation 有交集，但主问题不同。

### 4. `evaluation` 和 `serving` 不能只挂在末尾

如果没有 ToolEval、trace、verification、cost model，这条线很容易停留在 demo，而不是系统。

## 按问题选论文

如果你现在最关心的是：

- “怎么让 agent 更会用现有工具”
  - 先看 `ToolLLM`

- “怎么让 agent 自己造工具”
  - 先看 `CREATOR` 和 `LATM`

- “怎么避免工具越来越多后变乱”
  - 先看 `ToolLibGen`

- “怎么直接用 LLM 合成 API 实现”
  - 先看 `API Synthesis Using LLMs`

- “怎么把这些能力做成可运行系统”
  - 回到 agent/harness 官方实践资料

## 一句话总结

这 6 项材料不是同一层问题的重复，而是覆盖了一个完整系统的不同层：

- 用工具
- 造工具
- 管工具
- 综合实现
- 评估
- 运行

真正成熟的 agent/tool 系统，必须同时知道自己当前在这六层中的哪一层发力。
