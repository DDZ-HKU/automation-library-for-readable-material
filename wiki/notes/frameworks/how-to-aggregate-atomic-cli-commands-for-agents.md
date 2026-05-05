---
title: How to Aggregate Atomic CLI Commands for Agents
updated: 2026-04-11
status: active
---

# Summary

把原子化 CLI 命令直接交给 agent，只能解决“能不能操作”问题，不能解决“如何稳定扩展”问题。真正可持续的路线，是把原子命令逐步提升成任务工具，再把任务工具整理成工具库。ToolLLM、LATM 和 ToolLibGen 正好构成了这条演化线。

## Confirmed Understanding

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md) 已确认，tool use 不是单次 function call，而是一整条能力链。
- 同一概念页也确认，这条线会进一步分成：
  - tool use
  - tool making
  - tool library / tool asset reuse
- [[tool-use-tool-making-tool-library-branch]] / [../cases/tool-use-tool-making-tool-library-branch.md](../cases/tool-use-tool-making-tool-library-branch.md) 已确认，瓶颈会从调用工具逐步上移到生成工具，再上移到组织工具。

## Tacit Interpretation

- CLI 命令和 API 没本质区别，它们都是 agent 的外部动作接口。
- 所以同样的问题会重复出现：
  - 一开始：会不会调
  - 然后：有没有合适的中层工具
  - 最后：工具太多时怎么检索和组织
- 只把原子命令平铺给 agent，会让它拥有自由，但也让它长期背负过高的检索和组合负担。
- 真正成熟的系统不会停在“agent 会命令行”，而会继续往：
  - task facade
  - reusable script
  - tool library
  这几层发展。

## Four Patterns

### 1. Pipeline Wrapper

把固定顺序的原子命令包成脚本。

### 2. Task Facade

给高频任务提供更高层入口，比如：

- `kb search`
- `ops-check-handoff-readiness`

### 3. Maker-User Split

高能力 agent 造工具，低成本 agent 用工具。

### 4. Library Aggregation

工具变多后按功能聚类、抽共享逻辑、减少检索歧义。

## How To Think

判断某组 CLI 是否该聚合时，可以问：

1. 这组命令是否重复出现？
2. 顺序是否稳定？
3. 输出是否够稳定，能被后续步骤消费？
4. agent 是否已经经常在这些命令之间选错？

## How To Apply

- 保留真正通用的原子命令
- 把高频工作流优先封装成脚本
- 当脚本数量增加后，开始做工具库管理

## Links

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md)
- [[tool-use-tool-making-tool-library-branch]] / [../cases/tool-use-tool-making-tool-library-branch.md](../cases/tool-use-tool-making-tool-library-branch.md)
