---
title: How Agents Should Plan and Improve Atomic CLI Usage
updated: 2026-04-13
status: active
---

# Summary

原子化 CLI 不是不能直接交给 agent，但如果长期停留在原子层，agent 的主要成本会被消耗在检索、排序和误用上。最稳的演化路线，是把 CLI 从原子命令逐步提升成任务门面，再进一步进入 maker-user 分层和工具库聚合。

## Confirmed Understanding

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md) 已确认，tool use 不是单步 function call，而是一整条能力链。
- [[how-to-aggregate-atomic-cli-commands-for-agents]] / [how-to-aggregate-atomic-cli-commands-for-agents.md](how-to-aggregate-atomic-cli-commands-for-agents.md) 已确认，把原子 CLI 提升成任务工具是最稳的第一步。
- [[tool-use-tool-making-tool-library-branch]] / [../cases/tool-use-tool-making-tool-library-branch.md](../cases/tool-use-tool-making-tool-library-branch.md) 已确认，这条线的瓶颈会从 use 上移到 make，再上移到 library / governance。

## Tacit Interpretation

- CLI 和 API 对 agent 来说本质上是同类对象：外部动作接口。
- 所以 agent 的真正难点不是“会不会执行一个命令”，而是“如何在很多可能动作中做低错误率选择”。
- 一旦命令数量变多，规划质量就会比单命令能力更重要。
- 因此提升 agent 的 CLI 使用能力，最重要的不是加更多命令，而是减少检索歧义、稳定输出结构、明确调用层级。

## Planning Pattern

最稳的 planning loop 是：

1. retrieve
2. select
3. execute
4. observe
5. verify
6. continue or stop

## Five Patterns

1. atomic call
2. task facade
3. search-based planning
4. maker-user split
5. library aggregation

## How To Apply

- 原子 CLI 保底，不做主力
- 高频流程优先提升成任务门面
- 让高能力 agent 逐步生成项目专用脚本
- 当脚本开始增多，进入工具库聚合阶段

## Links

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md)
- [[how-to-aggregate-atomic-cli-commands-for-agents]] / [how-to-aggregate-atomic-cli-commands-for-agents.md](how-to-aggregate-atomic-cli-commands-for-agents.md)
- [[how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases]] / [how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)
- [[tool-use-tool-making-tool-library-branch]] / [../cases/tool-use-tool-making-tool-library-branch.md](../cases/tool-use-tool-making-tool-library-branch.md)
