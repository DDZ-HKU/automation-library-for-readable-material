# Harness 工程实践报告：可以有哪些组件与规则设计

日期：2026-04-14

## 这份报告回答什么

如果你要把一个 agent 系统从“模型会做点事”推进到“系统能稳定运行”，关键问题不是再换更强模型，而是：

- harness 应该由哪些组件构成
- 每个组件各自承担什么职责
- 规则应该落在哪一层
- 怎样避免把所有约束都堆进 prompt

这份报告就专门回答这些问题。

## 一句话结论

一个可用的 harness，至少不是“模型 + 一堆提示词”，而应当是一个分层系统：

1. `guide layer`
2. `tool / facade layer`
3. `sensor / verification layer`
4. `state / handoff layer`
5. `protocol / control layer`

再压缩一点就是：

**LLM 负责局部决策，harness 负责环境、边界、反馈、状态、交接与停止。**

## 一、Harness 工程到底在解决什么

Harness 工程要解决的，通常不是“模型能不能输出一段看起来合理的话”，而是下面这些系统问题：

- agent 是否知道该先读什么、先做什么
- agent 是否拿到了足够但不过载的上下文
- agent 是否有稳定工具可调
- agent 是否会在错误时被及时发现
- agent 是否有明确停止条件
- agent 中断后，是否能从结构化状态恢复

如果这些问题没有被系统层接管，模型再强，也很容易表现成：

- 方向乱跳
- 过早收尾
- 死循环
- 误用工具
- 产物存在但没验证

## 二、推荐的组件结构

### 1. Guide Layer

这是事前引导层。

典型组件：

- `AGENTS.md`
- repo rules
- skill files
- maps / reading guides
- task contracts

职责：

- 定义目标
- 定义默认顺序
- 定义边界
- 定义“什么问题该怎么进入”

设计规则：

- 保持短而强
- 用来规定方向，不用来代替验证
- 只写 agent 真会用到的规则
- 复杂决策不要全部塞进单个总文件

### 2. Tool / Facade Layer

这是动作层。

典型组件：

- atomic commands
- task scripts
- repo-local helper CLI
- MCP tools

职责：

- 提供外部动作接口
- 把高频动作提升成稳定任务入口

设计规则：

- atomic 保留灵活性
- facade 承担主流程
- 输入输出边界必须稳定
- 副作用要显式
- 不要给 agent 一个“功能很全但边界很糊”的工具

### 3. Sensor / Verification Layer

这是检测层。

典型组件：

- tests
- linters
- type checks
- review agents
- trace analysis
- readiness checks
- completion checklist middleware

职责：

- 判断当前做得对不对
- 判断是否可继续
- 判断是否可交接

设计规则：

- 能 deterministic 的先 deterministic
- 语义评估只补 deterministic 不覆盖的空白
- 让 agent 面对真实反馈，而不是自我感觉
- “做完了”必须是可检查状态，不是主观判断

### 4. State / Handoff Layer

这是状态外置层。

典型组件：

- workboard
- handoff files
- decision memo
- phase status
- contract artifacts

职责：

- 外置当前阶段状态
- 外置完成项、验证项、风险项
- 支撑跨 session 恢复

设计规则：

- 状态不要只存在 prompt 里
- handoff 不是日志，而是最小恢复状态包
- 每次交接至少写清：
  - 当前做到哪里
  - 已验证什么
  - 下一步是什么
  - 风险是什么

### 5. Protocol / Control Layer

这是运行边界层。

典型组件：

- runbook
- stop / continue rules
- retry policy
- approval gate
- timeout policy

职责：

- 定义默认执行循环
- 定义何时继续
- 定义何时停止
- 定义何时必须人工介入

设计规则：

- stop condition 要外置
- retry 次数要有限
- 高风险动作要有审批边界
- 不要让 agent 自己决定什么时候“差不多就停”

## 三、每层可以有哪些规则设计

### A. Guide 规则

可设计的规则包括：

- 查询顺序规则
  - 先读 `INDEX`
  - 先看 `wiki`
  - 不足再回 `raw`
- 任务进入规则
  - 先解释，再决定是否沉淀
  - 先判断问题属于 `concept / framework / output / raw`
- 风格规则
  - tacit page 必须区分 confirmed / interpretation / inference
- 主题边界规则
  - 哪类主题进入 `framework`
  - 哪类主题进入 `case`

### B. Tool / Facade 规则

可设计的规则包括：

- facade 候选规则
  - 高频重复
  - 顺序稳定
  - 输出应标准化
  - agent 容易选错
- 工具元信息规则
  - name
  - purpose
  - inputs
  - outputs
  - failure modes
  - side effects
  - risk level
- 暴露边界规则
  - 哪些工具只给高能力 agent
  - 哪些工具可默认暴露

### C. Sensor 规则

可设计的规则包括：

- completion gate
  - 未验证不得 claim complete
- readiness gate
  - handoff 前必须过检查
- loop detection
  - 同一对象重复修改超过阈值则提醒重审方案
- review layering
  - fast checks 先跑
  - expensive checks 后跑

### D. State / Handoff 规则

可设计的规则包括：

- handoff 格式规则
  - completed
  - verified
  - open risks
  - restart point
- decision memo 规则
  - 当前最稳判断
  - 当前主缺口
  - 下一步阅读顺序
- state externalization 规则
  - phase state 不得只存在对话上下文

### E. Protocol / Control 规则

可设计的规则包括：

- startup order
- default execution loop
- natural handoff definition
- early handoff cases
- retry cap
- approval requirement
- timeout / budget policy

## 四、最常见的 5 类实践模式

### 1. Feedforward Guides

在 agent 真开始前给出方向。

适合：

- repo 规则
- 目录地图
- task contract

### 2. Feedback Sensors

在生成后或中途提供纠偏。

适合：

- tests
- lints
- review
- readiness checks

### 3. Middleware Controls

在关键节点插入约束。

适合：

- completion checklist
- local context injection
- loop detection

### 4. Context Reset / Handoff

处理长任务与跨 session 连续性。

适合：

- long-running coding
- 多阶段 synthesis
- phase-based autonomous work

### 5. Deterministic Infrastructure First

先治理环境，再扩大 agent 自主性。

适合：

- coding agents
- enterprise-scale agent workflows
- unattended execution

## 五、不同场景下的组件重点

### 1. 单次问答型 agent

重点：

- guide
- basic tool layer
- minimal verification

### 2. coding agent

重点：

- guide
- facade / tools
- tests / lints / review
- state / handoff
- protocol

### 3. long-running autonomous agent

重点：

- state externalization
- reset / compaction / handoff
- stop condition
- readiness checks

### 4. enterprise orchestration

重点：

- deterministic infrastructure
- curated tool subsets
- tiered feedback
- hard retry cap
- role split

## 六、最容易犯的错误

- 把所有规则堆进 system prompt
- 让工具边界模糊
- 没有 handoff artifact
- 没有 verification gate
- 让 agent 自己决定什么时候停
- 高成本语义评估替代了低成本 deterministic checks
- 先加 agent 自主性，再补基础设施

## 七、一个最小可落地方案

如果你要从零开始搭一个实用 harness，最小方案可以是：

1. 一份短 guide
2. 少量稳定工具
3. 一个 facade 层
4. 一组 deterministic checks
5. 一个 handoff artifact
6. 一个 runbook

不要一上来就做复杂多代理系统。

## 八、对当前知识库仓库的映射

这套报告也能直接映射到当前仓库：

- guide：
  - `AGENTS.md`
  - skills
  - workflow guides
- facade：
  - `scripts/kb`
  - `scripts/pdf-to-md`
- sensor：
  - verification methods
  - `scripts/ops-check-handoff-readiness`
  - `scripts/ops-verify-continuation`
- state / handoff：
  - `ops/workboard.md`
  - `ops/handoff.md`
- protocol：
  - `ops/runbook.md`

## 一句话总结

Harness 工程真正要设计的，不是“再给模型一点提示”，而是：

**给 agent 一个有方向、有工具、有反馈、有状态、有边界的执行系统。**

## 关联页面

- [agent-harness-engineering.md](/Users/ddz/Documents/exp/wiki/concepts/agent-harness-engineering.md)
- [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
- [how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md)
- [how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops.md)
- [how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md)
