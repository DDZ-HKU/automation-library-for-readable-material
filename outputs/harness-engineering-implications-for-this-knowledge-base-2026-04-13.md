# Harness Engineering 对当前知识库设计的含义

日期：2026-04-13

## 这份 memo 回答什么

这批 harness 资料最重要的价值，不是再告诉我们“agent 需要环境、反馈和评估”，而是把一个更具体的问题推到台前：

**如果这个仓库要继续朝着 agent-first、long-running、verification-driven 的方向演化，哪些部分应该被当成 harness 设计，而不是普通文档或脚本？**

这份 memo 就专门回答这个问题。

## 一句话结论

对当前知识库来说，harness 不是外加层，而是仓库本身正在长出来的一条结构：

- `wiki/` 管知识
- `scripts/` 管高频动作
- `agent/skills/` 管规划与路由
- `ops/` 管长时运行、验证、停止和交接

也就是说：

**这个仓库已经不只是知识库，而是在逐步变成一个由知识层和 harness 层并行组成的 agent system。**

## 一、这批资料最直接推进了哪些理解

### 1. Harness 不是 prompt

Thoughtworks、OpenAI、Anthropic 和 LangChain 共同指向一个结论：

- prompt 只是 harness 的一部分
- 真正决定稳定性的，是外部化的 guides、sensors、环境、handoff、trace、eval 和 protocol

这对当前仓库的意义是：

- 不能把 `AGENTS.md` 当成唯一控制面
- 也不能把技能文件当成全部 harness

### 2. 长时运行需要协议，而不只是上下文

Anthropic 的长时运行材料和当前仓库的 `ops/runbook.md` 正好能对上：

- reset / compaction / handoff 必须明确区分
- stop condition 必须外置
- handoff 必须是最小恢复状态包

这意味着：

- `ops/` 不是辅助文档
- 它已经是当前仓库 long-running harness 的核心层

### 3. Trace 和 verification 不只是调试工具

LangChain 的材料把一个关键点讲得很清楚：

- trace 是 harness optimization 的数据源
- verification gate 是让 agent 面对真实反馈的卡口

这对当前仓库的意义是：

- `scripts/ops-check-handoff-readiness`
- `scripts/ops-verify-continuation`
- workboard 中每项的 verification method

这些都不只是流程装饰，而是当前仓库最接近 middleware / feedback sensors 的部件。

### 4. 工业级 agent scale 的真正底座是 deterministic infrastructure

Stripe Minions 这条 case 最值得带走的不是规模，而是顺序：

1. 先有 devbox、tooling、rules、feedback loop
2. 再让 agent 站到这个底座上

迁移到当前仓库，就是：

- 先让 `scripts/`、`ops/`、`skills/` 足够稳定
- 再继续扩大 agent 自主性

## 二、对当前仓库结构的具体映射

如果把当前仓库重新按 harness 视角压缩，可以得到这张图：

### 1. Knowledge Layer

- `wiki/sources/`
- `wiki/concepts/`
- `wiki/notes/`
- `outputs/`

职责：

- 显性知识
- 默会知识
- 阶段性成果

### 2. Feedforward Layer

- `AGENTS.md`
- `agent/skills/*`
- `agent/maps/*`
- repo-local docs / conventions

职责：

- 告诉 agent 该怎么进入问题
- 告诉 agent 先读什么、按什么顺序读
- 把 repo 结构变成 agent-readable

### 3. Feedback / Verification Layer

- verification commands in `ops/workboard.md`
- `scripts/ops-check-handoff-readiness`
- `scripts/ops-verify-continuation`
- review / dry-run style outputs

职责：

- 判断本轮工作是否真完成
- 判断能否 handoff
- 把“感觉完成”改成“验证完成”

### 4. Long-Running Control Layer

- `ops/runbook.md`
- `ops/workboard.md`
- `ops/handoff.md`
- `kb-autonomous-run`

职责：

- 定义默认执行循环
- 定义 stop / continue 规则
- 定义 handoff 条件
- 定义跨 session 恢复状态

## 三、这意味着当前仓库最该继续补什么

### 优先级 1：把更多高频约定从隐性经验转成机器可读 guides

比如：

- 哪类 query 默认先看 notes
- 哪类 output 应升格
- 哪类 source 应优先进入哪个主题线

这些如果只存在于“我们已经知道怎么做”，就还不够 harness 化。

### 优先级 2：把验证面继续外置

当前仓库已经有：

- workboard verification
- handoff readiness
- continuation verification

下一步应继续问：

- 哪些 ingest 结果也能有更明确的检查
- 哪些知识库更新能从“看起来合理”变成“有结构检查”

### 优先级 3：给 repo-local tools 增加更清楚的元信息层

当前 `scripts/` 已经在承担 facade 角色，但还缺：

- purpose
- inputs
- outputs
- side effects
- risk level

这也是从 tool governance 视角看最明显的下一步。

### 优先级 4：把 handoff artifact 继续标准化

当前 `ops/handoff.md` 已经够用，但如果以后 phase 更多、run 更长，可能要进一步模板化：

- completed
- verified
- open risks
- restart point

## 四、最重要的设计升级

这批资料带来的最大升级，不是“新增几个 framework 页”，而是让当前仓库的自我理解更清楚了：

- 这不是一个静态 wiki
- 也不是一个仅靠 prompt 驱动的 agent repo
- 它正在变成一个有：
  - knowledge layer
  - feedforward layer
  - feedback layer
  - long-running control layer
  的复合系统

如果后面继续演化，最稳的原则应该是：

**优先增强 deterministic infrastructure，再扩大 agent 自主性。**

## 五、对后续工作的直接建议

如果按这批 harness 材料来指导下一步仓库设计，最值得排进后续工作的不是“再写更多回答”，而是这三类动作：

1. 继续把 repo 约定整理成 agent-readable guides
2. 继续把关键判断整理成可执行 verification
3. 继续把自主运行时的 stop / continue / handoff 协议做得更明确

## 关联页面

- [agent-harness-engineering.md](/Users/ddz/Documents/exp/wiki/concepts/agent-harness-engineering.md)
- [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
- [how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)
- [how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md)
- [stripe-minions-as-infrastructure-first-agent-system.md](/Users/ddz/Documents/exp/wiki/notes/cases/stripe-minions-as-infrastructure-first-agent-system.md)
