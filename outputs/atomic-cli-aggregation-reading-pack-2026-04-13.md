# CLI 原子化聚合阅读包

日期：2026-04-13

## 这份首页怎么用

这不是第四份重复文档，而是一个阅读入口。

它的作用是：

- 帮不同角色快速找到该读哪一份
- 说明三份文档之间如何分工
- 让你在分发时不必再口头解释“先看哪份、为什么”

## 阅读包包含什么

### 1. 总览版

- [how-to-aggregate-atomic-cli-after-atomization-2026-04-13.md](/Users/ddz/Documents/exp/outputs/how-to-aggregate-atomic-cli-after-atomization-2026-04-13.md)

适合：

- 想先完整理解“原子化之后为什么还要聚合”的人
- 需要同时看分层、判据、方法和落地顺序的人

读完应拿走：

- 原子化不是终点
- 工具体系应分成 `Atomic / Facade / Planning / Governance`
- 最稳的推进顺序是先 facade，再治理

### 2. 管理者与架构师版

- [atomic-cli-aggregation-for-managers-and-architects-2026-04-13.md](/Users/ddz/Documents/exp/outputs/atomic-cli-aggregation-for-managers-and-architects-2026-04-13.md)

适合：

- 技术负责人
- 架构师
- 需要决定投资源在哪一层的人

读完应拿走：

- 为什么原子化后仍会出现检索、误用和资产失控问题
- 为什么 facade 是最值得优先投入的一层
- 什么时候该从“继续加脚本”切换到“工具治理”

### 3. 工程落地 Checklist 版

- [atomic-cli-aggregation-engineering-checklist-2026-04-13.md](/Users/ddz/Documents/exp/outputs/atomic-cli-aggregation-engineering-checklist-2026-04-13.md)

适合：

- 工程师
- agent harness 实现者
- 需要开始落脚本、补接口、做治理的人

读完应拿走：

- 哪些原子命令该进候选列表
- 第一批 facade 应该如何选
- 每个 facade 至少要补哪些字段
- 聚合后的验收标准是什么

## 推荐阅读顺序

### 如果你是第一次看这个主题

顺序：

1. 先看总览版
2. 再按角色补读管理版或工程版

原因：

- 先建立全局结构，再进入角色视角最稳

### 如果你是管理者或架构师

顺序：

1. 先看管理者与架构师版
2. 再回头看总览版
3. 只在需要落实施工时再给工程团队发 checklist 版

原因：

- 你最先需要的是决策框架，而不是实现细节

### 如果你是工程执行者

顺序：

1. 先看总览版
2. 再看工程 checklist 版

原因：

- 只看 checklist 容易知道“怎么做”，但不知道“为什么这么做”

## 三份文档如何分工

- 总览版负责解释：
  - 这件事是什么
  - 为什么要做
  - 应该怎么分层推进

- 管理版负责解释：
  - 应该投资源在哪
  - 什么时候该升级到下一层
  - 哪些是管理上最危险的误判

- 工程版负责解释：
  - 先做哪些 facade
  - 每个 facade 要补什么
  - 如何验收一轮聚合工作

它们的关系不是并列重复，而是：

- 总览版给全局结构
- 管理版给决策视角
- 工程版给执行视角

## 最短分发建议

如果你要把这套材料发给团队，可以直接这样分：

- 发给负责人：
  - 管理版
  - 如需背景，再附总览版

- 发给执行工程师：
  - 总览版
  - 工程 checklist 版

- 发给混合角色的小团队：
  - 先总览版
  - 再按角色看对应版本

## 一句话总结

这三份文档合起来，解决的是同一个问题的三个层次：

- 先讲清原子化之后为什么必须聚合
- 再讲管理上该怎么判断
- 最后讲工程上该怎么落地
