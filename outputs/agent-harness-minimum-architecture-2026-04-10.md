# Agent Harness 最小架构蓝图

日期：2026-04-10

## 结论

一个最小可用的 agent harness，不需要一开始就做成复杂平台。真正不可缺的只有七个部件：

1. task input
2. agent loop
3. tool runtime
4. state store
5. approval gate
6. trace logger
7. evaluator

如果这七个部件边界清楚，你就已经拥有一个可测、可调、可扩展的 agent 系统骨架。

## 一、最小闭环长什么样

最小闭环可以压成：

```text
user/task
  -> planner/router
  -> agent step
  -> tool call or final answer
  -> observation update
  -> repeat / stop
  -> evaluator
```

其中：

- LLM 负责当前步骤判断
- harness 负责状态、执行、权限、记录、停止和评分

不要把“规划”“执行”“验证”全部塞给一个无限自由的 prompt。它们应当是 loop 里的不同节点。

## 二、最小组件拆分

### 1. Task Input Layer

职责：

- 接收用户目标
- 规范化输入
- 标注风险级别
- 给任务分配 run id

必须输出：

- task id
- 原始目标
- 结构化目标摘要
- 风险标签
- 初始上下文

### 2. Agent Loop

职责：

- 读取当前状态
- 判断下一步动作
- 只产出一种受控动作：
  - final answer
  - tool call
  - request approval
  - request clarification
  - stop with failure

最关键的约束：

- 每个 step 只允许一个动作类型
- 不能同时“再想想、再搜搜、顺便执行”

### 3. Tool Runtime

职责：

- 接收结构化 tool call
- 执行工具
- 返回标准化结果
- 捕获错误和副作用

每个工具都应有：

- 明确名称
- 参数 schema
- 返回 schema
- 权限级别
- 幂等性说明

### 4. State Store

最少分三层：

- `prompt state`
  当前轮次让模型看见的上下文
- `working state`
  当前 run 的结构化中间结果
- `environment state`
  文件、数据库、外部系统等真实世界状态

关键原则：

- 不要让 LLM 上下文成为唯一状态源
- 真正重要的状态必须外置

### 5. Approval Gate

只要动作满足任一条件，就应该能经过审批节点：

- 高权限
- 高成本
- 不可逆
- 对外发送
- 可能泄露数据

Approval gate 不是“出问题再用”，而是架构内置节点。

### 6. Trace Logger

至少记录：

- task input
- 每轮 prompt 摘要
- 模型输出
- 工具调用参数
- 工具结果
- 审批事件
- 状态变更
- 最终结果

没有 trace，就没有可调试 agent。

### 7. Evaluator

最少分两层：

- run-level result evaluator
- harness-level regression evaluator

前者判断当前任务是否完成。
后者判断这次改动是否让系统整体变差。

## 三、最小状态设计

你可以先用下面这个结构：

```json
{
  "task": {
    "id": "task_001",
    "goal": "string",
    "risk_level": "low|medium|high"
  },
  "run": {
    "step_count": 0,
    "max_steps": 12,
    "status": "running"
  },
  "working_memory": {
    "facts": [],
    "open_questions": [],
    "candidate_actions": []
  },
  "tool_state": {
    "last_tool": null,
    "last_result": null
  },
  "result": {
    "final_answer": null,
    "artifacts": []
  }
}
```

核心不是字段多，而是：

- 哪些东西是模型可读的
- 哪些东西是系统真实状态
- 哪些东西必须跨轮持久化

## 四、最小工具接口设计

每个工具都尽量长成：

```json
{
  "tool": "search_docs",
  "arguments": {
    "query": "attention mechanism"
  }
}
```

返回：

```json
{
  "ok": true,
  "data": {...},
  "error": null,
  "side_effects": []
}
```

不要把工具返回做成模糊自由文本。越自由，后续节点越不稳。

## 五、最小停止条件

至少要有这五种 stop：

1. success
2. max steps reached
3. tool failure unrecoverable
4. approval required
5. missing information

否则 agent 会不断在低价值循环里消耗 token 和工具调用。

## 六、最小 eval 设计

最小 eval 集不要追求大，而要追求“覆盖关键失效模式”。

至少包含：

- 正常成功样本
- 边界样本
- 高风险审批样本
- 不该调用工具的样本
- 应调用但容易漏掉工具的样本
- 环境脏状态样本

评分至少看四个维度：

1. 任务完成度
2. 副作用控制
3. 工具使用是否合理
4. 停止行为是否正确

## 七、最小开发顺序

不要同时开发所有层。建议顺序是：

### 阶段 1

- 单代理
- 两到三个工具
- 明确 stop condition
- 全量 trace

### 阶段 2

- 加 approval gate
- 加 evaluator
- 补回归测试集

### 阶段 3

- 视情况再拆 router / planner / executor
- 视情况加多代理
- 视情况加长期记忆

## 八、最小架构最容易犯的错

### 1. 先做多代理，再想状态边界

这会让复杂度先爆炸。

### 2. 先调 prompt，再做 trace

这会让你看不到系统真正退化在哪。

### 3. 先做工具集合，再做 schema

这会得到一堆“模型会用，但系统不可控”的工具。

### 4. 把 evaluator 做成“必须按我的路径做”

这会压死 agent 的正确变通能力。

## 九、一句话蓝图

最小可用 agent harness 不是一个会自动做很多事的系统，而是一个能把：

- 当前任务
- 下一步动作
- 工具执行
- 状态更新
- 审批边界
- 轨迹记录
- 结果评分

串成稳定闭环的系统。
