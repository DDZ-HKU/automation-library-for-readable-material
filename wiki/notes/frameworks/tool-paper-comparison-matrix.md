---
title: Tool Paper Comparison Matrix
updated: 2026-04-13
status: active
---

# Summary

与 tool 相关的论文很容易被混成一类，但它们解决的问题分布在不同层次。最稳的比较方式，不是按年份或模型名排，而是按六个维度拆：`tool use`、`tool making`、`tool library`、`api synthesis`、`evaluation`、`serving`。

## Confirmed Understanding

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md) 已确认，当前主线至少可拆成 `tool use -> tool making -> tool library`。
- [[tool-use-tool-making-tool-library-branch]] / [../cases/tool-use-tool-making-tool-library-branch.md](../cases/tool-use-tool-making-tool-library-branch.md) 已确认，这条线的核心不是工具越来越多，而是瓶颈不断上移。
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md) 已确认，evaluation 与 serving 不是附属实现，而是系统层的一等问题。

## Tacit Interpretation

- 同样都叫“tool 论文”，有的在解决模型是否会用工具，有的在解决工具从哪来，有的在解决工具太多后怎么组织。
- 如果不先分层，读的时候就会把：
  - function calling
  - tool creation
  - API synthesis
  - tool governance
  混成一类。
- 最稳的比较方式是看论文到底在这六维里主攻哪一维，而不是看它用了多少“tool”这个词。

## Comparison Axes

1. `tool use`
2. `tool making`
3. `tool library`
4. `api synthesis`
5. `evaluation`
6. `serving`

## How To Apply

- 遇到新 tool 论文时，先给它打这六维标签。
- 不要先问“它是不是比上一篇更强”，先问“它是在同一层竞争，还是在补另一层空白”。

## Links

- [[tool-use-in-llms]] / [../../concepts/tool-use-in-llms.md](../../concepts/tool-use-in-llms.md)
- [[tool-use-tool-making-tool-library-branch]] / [../cases/tool-use-tool-making-tool-library-branch.md](../cases/tool-use-tool-making-tool-library-branch.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
- [[how-to-think-about-evaluation-and-serving-in-tool-agent-systems]] / [how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md](how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md)
