---
title: Agent Harness Engineering
updated: 2026-04-13
status: active
source_count: 4
---

# Summary

Agent harness engineering 关注的不是“模型还能不能更聪明”，而是“如何围绕模型建立一个可持续运行、可验证、可交接、可治理的执行系统”。在当前知识库里，这条主题线已经从最小单代理闭环，扩展到 coding-agent 外层 harness、长时运行 harness、trace-driven harness optimization，以及 Stripe Minions 这类工业级 orchestration 案例。

## Current Understanding

- harness 的核心分工是：
  - LLM 负责局部决策、语义压缩、候选比较、工具路由
  - harness 负责状态、环境、权限、反馈、审批、trace、eval 和 stop condition
- 在 coding agent 语境下，harness 不只是 prompt 或脚本，而是一整套外层 guides、sensors、tooling、runtime 和 workflow 协议。
- 最小 harness 要求：
  - 外部状态
  - 工具 schema
  - trace logger
  - evaluator
  - approval gate
  - 明确退出条件
- 长时运行 harness 进一步要求：
  - context 管理
  - handoff artifacts
  - 任务切块
  - generator / evaluator 分离
- trace-driven harness engineering 说明：
  - 很多问题不是模型能力不足，而是 feedforward / feedback / middleware 缺位
  - traces 是发现失败模式和调节 harness 的核心信号
- 工业级案例又说明：
  - devbox 基础设施
  - curated tool subsets
  - deterministic + agentic node 混合编排
  - 分层反馈与硬重试上限
  是规模化 coding agents 的关键部件
- Stripe Minions 这条案例进一步提醒：
  - deterministic infrastructure 才是 agent scale 的真正底座
  - agent 往往只是站在既有人类开发基础设施之上的执行层
- 这条主题线里还可以进一步分出两个稳定框架：
  - feedforward guides vs feedback sensors
  - traces / middleware / verification loops 驱动的 harness optimization
- 长时运行 harness 还进一步要求：
  - context reset
  - compaction
  - handoff artifact
  这三者要被当成不同机制来设计，而不是混成一个“续跑技巧”。

## Evidence

- 主要依据来自：
  - [[harness-engineering-for-coding-agent-users]] / [../sources/harness-engineering-for-coding-agent-users.md](../sources/harness-engineering-for-coding-agent-users.md)
  - [[harness-design-for-long-running-application-development]] / [../sources/harness-design-for-long-running-application-development.md](../sources/harness-design-for-long-running-application-development.md)
  - [[harness-engineering-exploiting-codex-in-the-age-of-agents]] / [../sources/harness-engineering-exploiting-codex-in-the-age-of-agents.md](../sources/harness-engineering-exploiting-codex-in-the-age-of-agents.md)
  - [[stripe-minions-ai-powered-developer-productivity]] / [../sources/stripe-minions-ai-powered-developer-productivity.md](../sources/stripe-minions-ai-powered-developer-productivity.md)

## Open Questions

- Stripe Minions 这类工业案例与当前仓库这种 knowledge-base harness 之间，哪些模式可直接迁移，哪些只适合大公司基础设施？

## Related Pages

- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
- [[agent-harness-minimum-architecture]] / [../notes/frameworks/agent-harness-minimum-architecture.md](../notes/frameworks/agent-harness-minimum-architecture.md)
- [[how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses]] / [../notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md](../notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md)
- [[how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops]] / [../notes/frameworks/how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops.md](../notes/frameworks/how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops.md)
- [[how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work]] / [../notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md](../notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md)
- [[how-to-think-about-evaluation-and-serving-in-tool-agent-systems]] / [../notes/frameworks/how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md](../notes/frameworks/how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md)
- [[stripe-minions-as-infrastructure-first-agent-system]] / [../notes/cases/stripe-minions-as-infrastructure-first-agent-system.md](../notes/cases/stripe-minions-as-infrastructure-first-agent-system.md)
