---
title: How to Use LLM Capabilities for Agents and Harness Engineering
updated: 2026-04-10
status: active
---

# Summary

开发 agents 时，最重要的判断不是“模型够不够聪明”，而是“哪些能力该交给 LLM，哪些稳定性必须由 harness 接管”。LLM 最适合承担局部决策、自然语言压缩、候选比较和工具路由；harness 则必须承担状态、权限、环境、反馈、轨迹和评估这些机械职责。

## Confirmed Understanding

- OpenAI 在 *A practical guide to building AI agents* 中把 agent 的基础归纳为 `model + tools + instructions`，并建议先从单代理做起，再逐步增加工具或代理分工。
- 同一指南还强调，复杂度管理的默认策略应是先把单代理能力拉满，只有在工具过载或逻辑分裂时再拆多代理。
- OpenAI 在 *Evaluation best practices* 中强调，LLM 系统必须采用 eval-driven development，并使用任务特定评估、日志、自动化评分和持续评估，而不能依赖“看起来可用”。
- 该评估指南还指出，LLM 更擅长比较、分类、按标准评分等判别任务，因此评估设计应尽量对齐这种强项。
- OpenAI 在 *Safety in building agents* 中明确建议：不要把不可信输入直接放进 developer messages；要用 structured outputs 限制数据流；高风险工具要有人类审批；要用 trace graders 和 evals 监控 agent 行为。
- Anthropic 在 *Demystifying evals for AI agents* 中把 eval harness 定义为负责指令、工具、并发运行、记录、评分与聚合的端到端基础设施，并强调稳定环境、隔离 trial、避免过度僵硬的 grader。
- OpenAI 在 *Harness engineering: exploiting Codex in the age of agents* 中把重点放在环境、意图表达和反馈回路，而不是把 agent 看成无约束自动化；文中强调“humans steer, agents execute”。

## Tacit Interpretation

- LLM 的真正优势不是“稳定地保存真理”，而是“在当前上下文里做一个足够好的下一步判断”。
- 因此 agent 不应被设计成“把整个系统正确性都压在模型身上”，而应被设计成“把模型限制在最擅长的局部决策位置上”。
- Harness 的价值不在于辅助模型，而在于把系统真正需要的机械可靠性从模型中剥离出来。
- 一个成熟的 agent 系统，本质上是“模型自由度”与“系统机械边界”之间的分工协定。
- 越是高风险、高状态性、强副作用的任务，越要把正确性从 prompt 转移到 harness 约束，而不是继续相信更长的 instructions。
- 所以 agent 工程的主战场并不是 prompt wording，而是：
  - 状态接口
  - 工具定义
  - 输出 schema
  - 审批节点
  - trace 记录
  - eval harness

## How To Think

设计 agent 时，先按下面这条线拆：

1. 哪些判断必须依赖 LLM 的语义弹性
2. 哪些约束必须从 LLM 身上拿走，收进 harness
3. 哪些动作有副作用，必须做审批或隔离
4. 哪些失败其实是环境或 grader 问题，而不是模型问题
5. 评估的对象到底是模型、agent harness，还是整个系统结果

一个好用的判断规则是：

如果某件事需要稳定、可复现、严格边界和抗注入，就优先交给 harness；如果某件事需要在不完全信息下做语义压缩、分类、比较和下一步选择，就交给 LLM。

## How To Apply

### 1. 设计 agent loop

- 把 agent 设计成观察 -> 决策 -> 行动 -> 再观察 的闭环
- 不要求模型一开始就给出完美大计划

### 2. 设计工具

- 工具名、参数、返回值必须稳定
- 工具越模糊，agent 越像在猜

### 3. 设计 harness

- 明确状态边界
- 设定退出条件
- 记录完整 trace
- 隔离 trial 环境
- 验证输出结果，而不是过度绑定固定步骤

### 4. 设计 eval

- 同时测“应该发生”和“不应该发生”
- 同时测正确完成与副作用控制
- 用人类反馈校准自动 grader

### 5. 设计安全边界

- 把外部文本视作不可信输入
- 用 structured outputs 和 schema 验证切断自由文本传播
- 对高风险工具调用保留审批节点

## To Be Verified

- 当前这篇框架主要基于 OpenAI 与 Anthropic 的官方实践文档，偏向“工程可落地性”，而不是学术型 agent taxonomy。
- 对多代理系统的最佳拆分粒度，仍需要结合具体业务和长期运行数据继续验证。
- 关于 harness 工程的更细粒度设计，例如长期记忆、事务回滚、分布式并发控制，目前知识库尚未专门建页。

## Links

- [OpenAI practical guide to building agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [OpenAI evaluation best practices](https://developers.openai.com/api/docs/guides/evaluation-best-practices)
- [OpenAI safety in building agents](https://developers.openai.com/api/docs/guides/agent-builder-safety)
- [OpenAI harness engineering](https://openai.com/fr-FR/index/harness-engineering/)
- [Anthropic demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [how-to-distinguish-architecture-optimization-and-systems-problems.md](how-to-distinguish-architecture-optimization-and-systems-problems.md)
- [[research-reading-and-decision-stack]] / [research-reading-and-decision-stack.md](research-reading-and-decision-stack.md)
