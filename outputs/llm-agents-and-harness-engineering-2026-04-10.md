# 如何利用 LLM 的特性来开发 Agents，以及 Harness 工程需要注意什么

日期：2026-04-10

## 结论

开发 agents 时，最重要的不是把 LLM 当成“更聪明的代码执行器”，而是把它当成一个：

- 擅长在不完全信息下做下一步决策的策略模块
- 擅长在候选方案之间做比较和判断的判别模块
- 擅长把自然语言目标压缩成可执行步骤的规划模块
- 但不擅长稳定保存长期状态、严格遵守隐含约束、或在无限自由里持续保持一致性的系统组件

所以 agent 工程的关键不是“让模型更自由”，而是：

- 把环境、工具、状态和反馈回路设计得足够机械
- 把模型真正擅长的部分留给模型
- 把模型不擅长的部分收进 harness

一句话说：

LLM 决定下一步，harness 决定它只能怎样安全、可测、可复现地走这一步。

## 一、要利用 LLM 的哪些原生特性

### 1. 利用它的“局部决策能力”，不要把它当成完美全局控制器

LLM 很适合在当前上下文下回答：

- 下一步最该做什么
- 该调用哪个工具
- 当前结果是否满足目标
- 该把任务交给哪个子代理

这意味着 agent 的基本 loop 应该围绕：

- 观察当前状态
- 选择下一步动作
- 执行动作
- 再观察新状态

而不是先要求模型在一开始就给出一个庞大、完美、一次成型的全局执行计划。

OpenAI 在其实践指南里把 agent 基础归成三件事：

- model
- tools
- instructions

并建议先从单代理开始，逐步加工具，而不是一上来就多代理编排。

来源：

- OpenAI, *A practical guide to building AI agents*：
  https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/

### 2. 利用它“更擅长判别而非无限生成”的特点

LLM 常常更擅长：

- 比较两个候选答案
- 判断某个输出是否满足标准
- 给结构化维度打分
- 判断该不该搜索、该不该升级、该不该调用工具

这意味着你应该多设计：

- classifier-style 节点
- router 节点
- judge 节点
- critique / self-check 节点

而不是把所有逻辑都做成开放式生成。

OpenAI 的 eval 最佳实践也明确建议：评估应尽量对齐 LLM 擅长的比较、分类、按标准评分等任务，而不是只做开放式生成评估。

来源：

- OpenAI, *Evaluation best practices*：
  https://developers.openai.com/api/docs/guides/evaluation-best-practices

### 3. 利用它“自然语言压缩控制”的能力

LLM 很适合把：

- 政策
- 工作流
- 用户目标
- 模糊任务边界

压缩成当前步骤的可执行指令。

所以 agent 很适合做：

- 高层任务拆解
- 工具选择
- 多代理分发
- 非结构化输入到结构化动作的过渡

但这依赖一个前提：

- 你必须把 prompt、tool schema、exit condition 和状态接口定义得清楚

如果这些边界模糊，模型就会把自由度用在你最不想让它自由发挥的地方。

### 4. 利用它“工具可塑性高”的特点，但不要给它模糊工具

LLM 可以学会调很多工具，但前提是：

- 工具名清楚
- 参数清楚
- 返回值稳定
- 工具之间边界明确

OpenAI 的代理指南强调，工具应该标准化、可复用、文档化，而且当工具数量增多时，应先考虑是否该拆代理。

这背后的原则是：

- agent 不是靠“工具多”变强
- 而是靠“工具边界清楚”变稳

## 二、真正的 agent 工程，不是 prompt 工程，而是 harness 工程

Harness 不是附属层，而是 agent 系统真正的骨架。Anthropic 对 eval harness 的定义很直接：它是那套端到端基础设施，负责提供指令和工具、运行任务、记录轨迹、打分并聚合结果。

来源：

- Anthropic, *Demystifying evals for AI agents*：
  https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents

对实际开发来说，harness 至少要负责七件事：

### 1. 状态控制

你必须决定哪些状态：

- 属于模型上下文
- 属于外部内存
- 属于环境真实状态

LLM 不应该成为长期状态的唯一载体。否则一旦上下文漂移、截断、污染，系统行为就会失控。

### 2. 工具调用控制

harness 应定义：

- 工具可见性
- 工具权限
- 工具调用格式
- tool result 的结构
- 何时需要人类确认

OpenAI 的 agent safety 文档明确建议：

- 不要把不可信输入直接放进 developer messages
- 用 structured outputs 限制节点间数据流
- 对高风险工具开启审批

来源：

- OpenAI, *Safety in building agents*：
  https://developers.openai.com/api/docs/guides/agent-builder-safety

### 3. 退出条件控制

一个 agent loop 如果没有明确 exit condition，就会出现：

- 无意义循环
- 工具乱用
- 过度搜索
- 过度思考

OpenAI 在代理指南里强调，run 本质上是一个 loop，必须定义清楚何时停止，比如：

- 产生最终输出
- 工具执行失败
- 达到最大轮次
- 遇到需人工判断的节点

### 4. 反馈回路控制

你不能只让 agent 做事，还要让它知道：

- 结果是否成功
- 失败原因是什么
- 当前状态与目标之间还差什么

没有显式反馈，agent 会越来越像“随机试错”而不是“闭环控制”。

### 5. 轨迹记录与可观测性

如果不记录 trace，你根本不知道问题来自：

- 模型判断错了
- 工具错了
- 环境脏了
- grader 错了
- harness 限制本身错了

所以 harness 必须至少记录：

- 输入
- 中间决策
- 工具调用
- 工具返回
- 环境变化
- 最终结果

### 6. 环境隔离

Anthropic 对 eval harness 的一个关键提醒是：

- 每次 trial 都要从干净环境开始
- 共享状态会制造虚假的成功或失败

如果多个运行共享：

- git 历史
- 缓存
- 文件残留
- 资源占用

你测到的往往不是 agent 能力，而是环境污染。

### 7. 评分与验证

好的 harness 不是只会“运行”，还必须会“判定”。

但验证不能太僵硬。Anthropic 特别指出，过度检查固定步骤会把 eval 变得脆弱，因为 agent 可能找到你没预料到、但同样正确的路径。

所以更好的原则是：

- 多评估结果
- 少评估死板路径

必要时对多维结果给 partial credit。

## 三、Harness 工程最常见的坑

### 1. 把模型问题和 harness 问题混在一起

很多“模型不行”其实是：

- 工具描述烂
- 状态接口乱
- grader 不合理
- 环境不可复现
- 退出条件没写清

Anthropic 给过一个很典型的例子：某 agent 分数很低，后来发现是 grading 太死、任务说明含糊、环境有随机性，修完后分数大幅上升。问题不完全在模型。

### 2. 只测“应该发生什么”，不测“不该发生什么”

如果你只测：

- 什么时候该搜索

却不测：

- 什么时候不该搜索

那最后往往会得到一个“见什么都搜”的 agent。

这类问题在工具调用、升级人工、写数据库、发消息等动作上都一样。

### 3. 用 vibe 代替 eval

“看起来还行”不是 eval。

官方建议很一致：

- 早做 eval
- 用真实分布
- 记录日志
- 持续评估

否则 agent 系统一复杂，你根本不知道改进来自哪里，退化又来自哪里。

### 4. 一开始就多代理

多代理不是默认更高级，而是默认更复杂。

OpenAI 的建议是先把单代理做强，只有在：

- prompt 逻辑过长
- 工具过载
- 职责明显分裂

时再拆。

### 5. 让不可信文本直接驱动高权限动作

这会把 prompt injection 直接放大成真实系统风险。

你需要把：

- 用户输入
- 外部网页
- RAG 文档
- 搜索结果

都视作不可信数据源。

对这些输入，最稳的方法不是“让模型自己小心”，而是：

- 用户消息隔离
- structured outputs
- schema 验证
- tool approval
- guardrails

## 四、如何把这些原则落成一套开发方法

你可以把 agent 开发压成下面这条线：

### 1. 先做单代理最小闭环

只保留：

- 一个模型
- 最少的工具
- 清楚的结束条件
- 可观测 trace

先测通一个真实任务，不要先追求宏大编排。

### 2. 先做 harness，再调 prompt

先固定：

- 状态边界
- 工具 schema
- 输出格式
- 失败处理
- trace 记录
- eval 数据集

再去调提示词。否则你永远不知道问题到底出在哪一层。

### 3. 用 eval 驱动，而不是凭感觉迭代

最小 eval 集就该覆盖：

- 成功样本
- 边界样本
- 对抗样本
- 不该触发工具的样本
- 应该触发但容易漏掉的样本

### 4. 先评估结果，再视情况评估过程

优先看：

- 任务完成了吗
- 副作用可接受吗
- 输出正确吗
- 工具使用是否过度或不足

只有在需要调试时，再看细粒度 trace 和中间步骤。

### 5. 把“人类判断”设计成系统节点

人类不该被当成兜底噪音，而该被当成：

- 高风险批准节点
- 歧义裁决节点
- 评估校准节点

这才是 agent 系统里最值钱的人类位置。

## 五、一句话方法论

开发 agents 时，要把 LLM 当成一个高弹性的“下一步决策器”，而不是一个完整可靠的软件系统；你真正要工程化的，是围绕它的 harness：

- 约束输入
- 约束输出
- 管住工具
- 隔离环境
- 记录轨迹
- 设计 eval
- 用机械反馈环把模型自由度收敛成可控行为

## 参考来源

- OpenAI, *A practical guide to building AI agents*  
  https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/
- OpenAI, *Evaluation best practices*  
  https://developers.openai.com/api/docs/guides/evaluation-best-practices
- OpenAI, *Safety in building agents*  
  https://developers.openai.com/api/docs/guides/agent-builder-safety
- OpenAI, *Harness engineering: exploiting Codex in the age of agents*  
  https://openai.com/fr-FR/index/harness-engineering/
- Anthropic, *Demystifying evals for AI agents*  
  https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
