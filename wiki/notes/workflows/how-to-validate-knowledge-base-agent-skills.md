---
title: How to Validate Knowledge Base Agent Skills
updated: 2026-04-13
status: active
---

# Summary

知识库技能层不应只靠“文件存在”就默认可用。更稳的做法是分两步验证：先做静态结构校验，再做基于真实请求类型的 dry run 路由测试。这样可以把“skill 已创建”和“skill 真能把请求导到正确动作”区分开，避免 repo-local skills 长期漂移。

## Confirmed Understanding

- `outputs/knowledge-base-agent-skills-test-report-2026-04-10.md` 已确认，第一版知识库技能层的有效验证至少包含两部分：
  - 静态结构校验
  - dry run 路由测试
- 当前知识库技能层的关键对象包括：
  - `agent/skills/`
  - `agent/playbooks/`
  - `agent/maps/`
- 当前技能链的关键依赖包括：
  - `wiki/INDEX.md`
  - `kb-locate`
  - `kb-synthesize-output`
  - `wiki/log.md`

## When To Use

在以下情况应运行这套 workflow：

- 新建或修改了 `kb-route`
- 新建或修改了 `kb-ask`、`kb-teach`、`kb-guide`、`kb-synthesize-output`
- 新增了 playbook 或 map，并改变了技能职责
- 准备让一套新技能进入真实使用

## Validation Flow

### 1. 静态结构校验

先检查结构是否齐全：

- 目标 skill 文件存在
- frontmatter 合法
- 关键调用钩子存在
- 技能之间的依赖对象已创建

至少应确认：

- `agent/skills/` 中相关技能存在
- `agent/playbooks/` 中所需模板存在
- `agent/maps/` 中所需导航文件存在

### 2. 路由规则校验

检查 skill 描述和 route 规则是否足够显式。

重点看：

- 直接问答是否会进入 `kb-ask`
- 教学请求是否会进入 `kb-teach`
- 阅读路径请求是否会进入 `kb-guide`
- 沉淀判断是否会进入 `kb-synthesize-output`

### 3. Dry Run 场景测试

至少准备一组代表性请求，覆盖：

- 直接知识问题
- 深讲请求
- 产物讲解请求
- 阅读路径请求
- 沉淀判断请求
- 混合意图请求

每条请求都要记录：

- 请求文本
- 期望路由
- 实际结果
- 如果失败，失败原因是什么

### 4. 修正规则

如果测试发现问题，不要只记在报告里，要立刻更新：

- route 规则
- skill 描述
- playbook 模板
- 或 map 导航

### 5. 进入真实回合验证

静态校验和 dry run 通过后，不应停在纸面验证，还应继续：

- 用真实知识库问题连续跑多轮
- 观察 skill 是否会互相抢职责
- 观察 `kb-synthesize-output` 是否真的能带动 `INDEX/log` 更新

## Minimal Test Set

一轮最小测试至少应覆盖这 6 类：

1. 直接知识问题
2. 教学展开
3. output 讲解
4. 阅读路径
5. 沉淀判断
6. 混合意图

## Pass Criteria

可以认为技能层进入可用状态，当且仅当：

- 结构校验通过
- 主要请求类型都有明确路由
- 代表性 dry run 基本通过
- 发现的问题已回写到 skill 规则，而不是只留在测试报告里

## Common Mistakes

- 只检查文件是否存在，不检查路由是否真的清晰
- 只测单一请求类型，不测混合意图
- 发现问题后只写报告，不更新 skill 规则
- 把 dry run 当成终点，不进入真实回合测试

## Source Trace

这页主要由以下 output 升格而来：

- [../../../outputs/knowledge-base-agent-skills-test-report-2026-04-10.md](../../../outputs/knowledge-base-agent-skills-test-report-2026-04-10.md)

## Links

- [../../../outputs/knowledge-base-agent-skills-test-report-2026-04-10.md](../../../outputs/knowledge-base-agent-skills-test-report-2026-04-10.md)
- [../workflows/how-to-promote-outputs-into-frameworks-or-workflows.md](how-to-promote-outputs-into-frameworks-or-workflows.md)
