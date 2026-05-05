---
title: Research Reading and Decision Stack
updated: 2026-04-09
status: active
---

# Summary

这页是当前默会知识框架的总导航。它把“读论文、分辨问题类型、识别机制与瓶颈、形成研究决策”串成一条连续流程，避免把这些能力分散成互相孤立的技巧。

## The Stack

当前推荐的研究阅读与决策顺序是：

1. 先确认你在看什么层次的问题
2. 再判断论文真正改了什么机制
3. 再识别它暴露或缓解了什么瓶颈
4. 再判断它的可迁移价值
5. 最后才把这些判断转成下一步研究动作

## Layer 1: Problem Typing

先用这页给论文打主标签：

- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [how-to-distinguish-architecture-optimization-and-systems-problems.md](how-to-distinguish-architecture-optimization-and-systems-problems.md)

核心问题：

- 这是架构问题、优化问题，还是系统问题？

如果这一步不做，后面的所有判断都容易混层。

## Layer 2: Mechanism and Bottleneck Reading

再用这页去读论文本身：

- [[how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value]] / [how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value.md](how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value.md)

核心问题：

- 作者真正改了哪条因果链？
- 它暴露的真实瓶颈是什么？
- 这篇工作的价值，离开 benchmark 后还剩什么？

如果论文本身是 tool / agent system 论文，而不是纯模型论文，再补这页：

- [[how-to-read-a-tool-paper-for-system-construction]] / [how-to-read-a-tool-paper-for-system-construction.md](how-to-read-a-tool-paper-for-system-construction.md)

核心问题：

- 它的系统最小闭环由哪些部件组成？
- 部件之间如何分工？
- 哪一层才是真正的系统瓶颈？

## Layer 3: Topic-Specific Interpretation

如果论文属于你已经在追的主题线，再进入案例页：

- [[tacit-knowledge-on-rnn-to-transformer-transition]] / [../cases/tacit-knowledge-on-rnn-to-transformer-transition.md](../cases/tacit-knowledge-on-rnn-to-transformer-transition.md)

核心问题：

- 这篇新论文会把现有主题线往哪一层推进？
- 它是在补旧范式，还是在推动范式转移？

## Layer 4: Repository Action

读完后不要停在“我懂了”，而要决定知识库动作：

- 如果主要是显性新事实：更新 `wiki/sources/` 和 `wiki/concepts/`
- 如果主要带来新判断框架：更新 `wiki/notes/frameworks/`
- 如果主要深化某条知识线：更新 `wiki/notes/cases/`
- 如果主要形成一次性成果：输出到 `outputs/`

## Practical Workflow

一篇新论文进入知识库时，建议至少回答下面五个问题：

1. 这篇论文属于哪一层问题？
2. 它真正改变了什么机制？
3. 它暴露或缓解了什么瓶颈？
4. 它最值得迁移的部分是什么？
5. 它应该更新知识库的哪一层？

## Decision Rules

- 如果你还说不清“它属于哪一层问题”，先不要急着总结结论。
- 如果你说不清“它改变了什么机制”，先不要把它当成重大进展。
- 如果你说不清“它的价值能迁移到哪”，先不要高估它的长期意义。
- 如果你说不清“它该更新知识库哪一层”，说明你的理解还停在表面。

## What This Stack Is For

- 帮你把阅读论文从“被动吸收信息”变成“主动形成判断”
- 帮你把判断结果稳定沉淀回知识库
- 帮你减少被单次指标、流行叙事和作者表述方式带偏的风险

## Links

- [[tacit-knowledge-layer]] / [tacit-knowledge-layer.md](tacit-knowledge-layer.md)
- [[how-to-distinguish-architecture-optimization-and-systems-problems]] / [how-to-distinguish-architecture-optimization-and-systems-problems.md](how-to-distinguish-architecture-optimization-and-systems-problems.md)
- [[how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value]] / [how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value.md](how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value.md)
- [[tacit-knowledge-on-rnn-to-transformer-transition]] / [../cases/tacit-knowledge-on-rnn-to-transformer-transition.md](../cases/tacit-knowledge-on-rnn-to-transformer-transition.md)
