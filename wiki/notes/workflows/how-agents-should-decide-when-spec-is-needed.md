---
title: How Agents Should Decide When Spec Is Needed
updated: 2026-05-05
status: active
---

# Summary

这个仓库里的 spec 不应因为“看起来像新功能”就频繁触发。更稳的边界是：只有当改动会留下新的长期维护负担时，agent 才应考虑写 spec。对不新增长期维护对象的局部修补，应直接执行；对只新增一个小而清楚的长期对象，可用轻量 spec；只有当改动会改变默认行为、规则系统或工具层结构时，才进入 full spec。

## Why This Guide Exists

如果 spec 触发过宽，知识库维护会出现两个问题：

- 大量本应直接做完的局部维护，被升级成高摩擦设计流程
- agent 开始把 spec 当成“安全动作”，而不是“真正需要的长期治理动作”

这会让：

- 断链修复
- alias 回填
- 局部 update
- `INDEX` / `log` 同步
- 页尾链接收缩

这些原本应该低成本完成的工作，被不必要地抬高。

## Core Test

判断是否需要 spec，先问一个问题：

**这次改动会不会新增一个以后要持续维护的对象？**

如果答案是否定的，默认不要触发 spec。

## What Counts as Long-Term Maintenance Burden

下面 4 类对象，都会形成新的长期维护负担：

### 1. New Persistent Object

例如：

- 新脚本
- 新 workflow guide
- 新 report 类型
- 新目录职责
- 新入口技能或新入口页

### 2. New Default Behavior

例如：

- 改变 agent 的默认动作顺序
- 改变默认查询顺序
- 改变默认维护入口

### 3. New Rule System

例如：

- 新的链接预算机制
- 新的 stale/orphan 判定体系
- 新的 output promotion 边界

### 4. New Tool Entry

例如：

- 新命令
- 新子命令
- 新的 facade 入口

## The Three Levels

### 1. No Spec

条件：

- 不新增长期维护对象
- 只是修已有对象
- 不改变默认行为

典型任务：

- 修断链
- 补 alias
- 局部文案修改
- 单页链接减重
- 更新 `wiki/INDEX.md`
- 更新 `wiki/log.md`
- 对现有规则做极小局部修补，但不形成新规则系统

默认动作：

- 直接执行
- 必要时写最小变更说明
- 不进入 spec 流程

### 2. Light Spec

条件：

- 新增长期维护对象
- 但范围小、耦合低、语义清楚
- 不跨两层以上
- 不改变仓库总模式

典型任务：

- 给现有 `scripts/kb` 增加一个轻量子命令
- 新增一页边界清晰的 workflow guide
- 引入一个新的固定 report 产物

默认动作：

- 写短 spec
- 重点回答：
  - 为什么要新增这个对象
  - 它改变哪条边界
  - 它不负责什么

### 3. Full Spec

条件：

- 新增长期维护对象
- 且会改变默认行为、规则系统或工具层结构
- 或同时新增多个对象并跨层联动

典型任务：

- 新的知识操作模式
- 新的工具层结构
- 新的自动化治理闭环
- 新的长期 protocol / facade / guide 组合

默认动作：

- 进入完整 spec 流程
- 必须明确长期维护成本、分层职责和非目标

## Default Decision Rules

可以按这个顺序判断：

1. 这次是否新增了一个以后要持续维护的对象？
2. 如果没有 -> `No Spec`
3. 如果有，再问它是否会改变默认行为、规则系统或工具层结构？
4. 如果不会 -> `Light Spec`
5. 如果会 -> `Full Spec`

## Negative Rules

下面这些情况，不应单独触发 full spec：

- 改动看起来“有点新”
- 文件数变多了
- 页面之间多加了几条链接
- 需要更新 `INDEX` / `log`
- 只是为了让自己更安心

也就是说，**“不确定就先写 full spec” 不是这个仓库的默认策略。**

## Common Misfires

- 把局部维护误判成新机制设计
- 把一次修补误判成新规则系统
- 只因为新增了一个文件，就自动升级成 full spec
- 把“避免出错”错误地等同于“必须先写 spec”

## Rule of Thumb

可以把这页压成一句话：

**只有当改动会留下新的长期维护负担时，才考虑 spec；否则直接做。**

## Source Trace

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md)
- [README.md](/Users/ddz/Documents/exp/README.md)
- [how-to-run-ingest-query-lint-update-in-this-repo.md](how-to-run-ingest-query-lint-update-in-this-repo.md)
- [how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md](how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md)

## Related Pages

- [[how-to-run-ingest-query-lint-update-in-this-repo]] / [how-to-run-ingest-query-lint-update-in-this-repo.md](how-to-run-ingest-query-lint-update-in-this-repo.md)
- [[how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol]] / [how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md](how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md)
- [[how-agents-should-govern-links-and-diffs-in-this-knowledge-base]] / [how-agents-should-govern-links-and-diffs-in-this-knowledge-base.md](how-agents-should-govern-links-and-diffs-in-this-knowledge-base.md)

## Links

- [../../INDEX.md](../../INDEX.md)
- [../../../docs/superpowers/specs](/Users/ddz/Documents/exp/docs/superpowers/specs)
- [../../../docs/superpowers/plans](/Users/ddz/Documents/exp/docs/superpowers/plans)
