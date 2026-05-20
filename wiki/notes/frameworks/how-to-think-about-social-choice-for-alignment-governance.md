---
title: How to Think About Social Choice for Alignment Governance
updated: 2026-05-06
status: active
---

# Summary

当“人类偏好”不再来自单个反馈者，而来自多个标注者、多个用户群体或多个利益相关方时，对齐问题就进入社会选择问题域。这里的关键不再只是“学得准不准”，而是“不同偏好如何被聚合、谁的偏好更有权重、以及聚合规则本身会不会扭曲结果”。

## Confirmed Understanding

- [[economics-and-alignment]] / [../../concepts/economics-and-alignment.md](../../concepts/economics-and-alignment.md) 已确认，群体偏好天然不一致，无法被视为单一稳定目标。
- [../../../outputs/economics-and-alignment-for-rlhf-and-agents-2026-05-06.md](../../../outputs/economics-and-alignment-for-rlhf-and-agents-2026-05-06.md) 已确认，Arrow 不可能定理的启发是：偏好聚合没有完美且无代价的规则。
- [[game-theory-for-ai-interaction]] / [../../concepts/game-theory-for-ai-interaction.md](../../concepts/game-theory-for-ai-interaction.md) 已确认，规则一旦确定，主体会开始适应这些规则。

## The Core Reframe

很多对齐讨论默认存在一个“人类偏好目标”，好像问题只是模型能否学到它。

社会选择视角会先打断这个假设：

- 偏好来自谁？
- 不同人的偏好是否可兼容？
- 聚合规则为什么是现在这个，而不是另一个？
- 聚合过程会不会系统性偏袒某类人、某类风险取向或某类组织目标？

## Three Governance Questions

### 1. Constituency

到底哪些人的偏好进入系统？

### 2. Aggregation Rule

这些偏好是怎样被压成一个训练或部署目标的？

### 3. Legitimacy

为什么这个聚合方式可以被认为是合理的？

## Failure Modes

### 1. False Unanimity

系统假装存在统一的人类偏好，其实只是把差异抹平了。

### 2. Hidden Weighting

某些群体的偏好被默认赋予更高权重，但这一点没有被显式说明。

### 3. Governance by Convenience

最后被优化的不是合理聚合后的偏好，而是最容易采集、最容易评分、最容易部署的偏好代理。

## How To Apply

设计 alignment pipeline 时，至少问：

1. 偏好样本来自哪些人？
2. 聚合规则是否被写清楚？
3. 当前 reward 或 policy 更像在代表“多数偏好”、平台偏好，还是风险规避偏好？
4. 如果利益相关方发生冲突，系统准备如何处理？

## Rule of Thumb

**一旦系统说自己在对齐“人类偏好”，就必须先说明它在聚合哪些人、按什么规则聚合。**

## Source Trace

- [[economics-and-alignment]] / [../../concepts/economics-and-alignment.md](../../concepts/economics-and-alignment.md)
- [[game-theory-for-ai-interaction]] / [../../concepts/game-theory-for-ai-interaction.md](../../concepts/game-theory-for-ai-interaction.md)
- [../../../outputs/economics-and-alignment-for-rlhf-and-agents-2026-05-06.md](../../../outputs/economics-and-alignment-for-rlhf-and-agents-2026-05-06.md)

## Links

- [[agi-theme-stack]] / [agi-theme-stack.md](agi-theme-stack.md)
- [[how-to-think-about-mechanism-design-for-rlhf-and-agent-systems]] / [how-to-think-about-mechanism-design-for-rlhf-and-agent-systems.md](how-to-think-about-mechanism-design-for-rlhf-and-agent-systems.md)
- [[how-to-think-about-behavioral-economics-for-human-feedback]] / [how-to-think-about-behavioral-economics-for-human-feedback.md](how-to-think-about-behavioral-economics-for-human-feedback.md)
