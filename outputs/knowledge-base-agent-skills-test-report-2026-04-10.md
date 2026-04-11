# Knowledge Base Agent Skills Test Report

日期：2026-04-10

## 范围

本次测试验证 repo-local 知识库技能层的第一版实现，覆盖：

- `kb-route`
- `kb-ask`
- `kb-teach`
- `kb-guide`
- `kb-locate`
- `kb-explain-page`
- `kb-synthesize-output`

测试方式分两层：

1. 静态结构校验
2. dry run 路由测试

## 静态校验结果

已确认：

- `agent/skills/` 下 7 个技能文件均已创建
- `agent/playbooks/` 下 4 个模板文件均已创建
- `agent/maps/` 下 3 个导航文件均已创建
- 7 个技能文件都包含合法 frontmatter
- 关键调用钩子存在：
  - `wiki/INDEX.md`
  - `kb-locate`
  - `kb-synthesize-output`
  - `wiki/log.md`
- `kb-locate` 已明确固定检索顺序：
  - `INDEX -> concepts -> sources -> notes -> outputs -> raw`

结论：

- 静态结构通过

## Dry Run 场景

### 场景 1

请求：

> attention 和 Transformer 的差别是什么？

期望路由：

- `kb-route -> kb-ask`

结果：

- 通过

原因：

- 属于直接知识问题
- 不要求教学展开或阅读路径

### 场景 2

请求：

> 细讲 Bahdanau attention 为什么重要

期望路由：

- `kb-route -> kb-teach`

结果：

- 通过

原因：

- 含有“细讲”
- 请求的是解释与判断，不是简答

### 场景 3

请求：

> 把 rnn-transformer-research-decision-memo 讲懂

期望路由：

- `kb-route -> kb-teach`

结果：

- 初版规则偏隐含，已补强后通过

原因：

- 这是典型的“围绕产物做讲解”
- 已在 `kb-route` 中显式加入：
  - “拆解这个产物”
  - “讲懂这份 memo”
  - “详细解释这页输出”

### 场景 4

请求：

> 我应该从哪几页开始理解 RNN 到 Transformer 这条线？

期望路由：

- `kb-route -> kb-guide`

结果：

- 通过

原因：

- 明确是阅读路径请求

### 场景 5

请求：

> 先看哪个 output 最能帮我接上昨天的研究？

期望路由：

- `kb-route -> kb-guide`

结果：

- 初版规则偏隐含，已补强后通过

原因：

- 这是“产物导航”，不是直接问答
- 已在 `kb-route` 中显式加入：
  - “先看哪个 output”
  - “已有哪份产物最相关”

### 场景 6

请求：

> 这个回答值得存成产物吗？

期望路由：

- `kb-route -> kb-synthesize-output`

结果：

- 通过

原因：

- 属于显式沉淀判断

### 场景 7

请求：

> attention 是什么，以及我下一步该读什么？

期望路由：

- 优先 `kb-guide`

结果：

- 初版未写明混合意图优先级，已补强后通过

原因：

- 这类请求包含问答和导航双意图
- 当前规则已明确：
  - 同时出现“这是什么”和“下一步读什么”时，优先 `kb-guide`

## 发现的问题

### 问题 1：产物讲解路由不够显式

状态：

- 已修复

修复内容：

- 在 `kb-route` 中新增了针对 output/memo 讲解的显式映射

### 问题 2：混合意图请求的优先级未写清

状态：

- 已修复

修复内容：

- 在 `kb-route` 中补充：
  - 同时包含“是什么”和“下一步读什么”时，优先走 `kb-guide`

## 当前结论

第一版技能层已经具备可用性，尤其是这三条高频链路：

- `kb-route -> kb-ask`
- `kb-route -> kb-teach`
- `kb-route -> kb-guide`

同时，`kb-synthesize-output` 已经为后续把高价值回答回写到知识库提供了明确规则。

## 仍需进一步测试的点

- 用真实对话连续跑 3 到 5 轮，观察 `ask` 与 `teach` 是否还会互相抢职责
- 用一个全新主题验证 `kb-locate` 是否会过度依赖旧高价值页
- 用一次真实沉淀流程验证 `kb-synthesize-output -> INDEX/log` 的实际执行质量

## 一句话结论

这套技能层已经可以进入真实使用阶段；下一步不该再停留在结构测试，而应开始拿真实知识库问题做连续回合验证。
