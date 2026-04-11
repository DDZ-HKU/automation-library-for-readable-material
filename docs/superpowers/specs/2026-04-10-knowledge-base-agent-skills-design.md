# Knowledge Base Agent Skills Design

日期：2026-04-10

## 目标

为当前知识库补一层面向 agent 的 skills 体系，使 agent 在处理知识库请求时不再“临时从零检索”，而是按固定工作流完成：

- 基于 `wiki/` 与 `outputs/` 快速问答
- 围绕某个知识页或产物做更细的讲解、拆解与延伸
- 自动决定该读哪些页面、该走哪种回答链
- 在有长期价值时，把结果沉淀回 `outputs/` 或 `wiki/notes/`

本设计以 `skills` 为中心，不把重点放在脚本工具。工具最多作为 skill 内部的辅助，而不是系统主入口。

## 非目标

- 不设计数据库、向量库或独立检索服务
- 不依赖外部 Web UI 或知识图谱系统
- 不把现有 `AGENTS.md` ingest/query/lint 逻辑替换掉
- 不为每个主题单独做定制 skill

## 现状判断

当前仓库已经形成四层知识资产：

- `wiki/sources/`：资料级摘要，解决“原文说了什么”
- `wiki/concepts/`：主题级知识，解决“目前确认了什么”
- `wiki/notes/`：默会知识层，解决“如何思考、判断、应用”
- `outputs/`：面向具体问题的产物，解决“为某次任务产出了什么”

当前缺口不是再加一层目录，而是给 agent 增加一组稳定可复用的工作流技能，使其：

- 先知道去哪里找
- 再知道该如何回答
- 最后知道什么结果要沉淀

## 设计原则

### 1. 入口技能少，执行技能清晰

高频只暴露少量入口 skill，避免让 agent 每次都在很多技能之间犹豫。复杂工作交给执行技能承接。

### 2. 优先复用 wiki，而不是回原始资料

所有 query/teach 类 skill 默认先读：

1. `wiki/INDEX.md`
2. 相关 `wiki/` 页面
3. 相关 `outputs/`
4. wiki 不足时才回 `raw/`

### 3. 明确区分“回答”和“讲解”

- 问答 skill 追求快速、准、基于现有知识页
- 讲解 skill 追求结构化解释、误区澄清、应用方式和思考路径

### 4. 让 skill 能驱动知识沉淀

高价值结果不能只停留在对话里。skills 必须包含“是否沉淀”和“沉淀到哪里”的判断规则。

### 5. 技能职责单一，但允许调用链

每个 skill 只负责一个清晰动作；复杂任务通过 skill 串联完成，而不是让单个 skill 同时承担定位、问答、讲解、沉淀四种职责。

## 技能架构

采用双层结构：

- 第一层：面向用户意图的入口技能
- 第二层：面向知识动作的执行技能

### 第一层：入口技能

#### 1. `kb-ask`

用途：

- 用户直接提问
- 用户要比较、总结、判断、解释某个问题
- 用户默认想要一个基于现有知识库的回答

核心职责：

- 先定位相关知识页
- 基于 `wiki/` 和 `outputs/` 回答
- 明确区分已确认内容、补充信息、待验证推断
- 如结果有长期价值，转给沉淀技能

不负责：

- 长篇教学式展开
- 主题导航设计
- ingest 新资料

#### 2. `kb-teach`

用途：

- 用户说“细讲”“教我怎么理解”“教我如何思考”
- 用户希望围绕某个知识页或某个产物做更深讲解
- 用户需要应用方法、误区提醒、迁移判断

核心职责：

- 优先读取 `wiki/notes/`
- 必要时回链到 `concepts`、`sources`、`outputs`
- 输出分层讲解，而不是简单摘要
- 显式区分：显性知识、默会知识解读、待验证推断

不负责：

- 普通简短问答
- 资料 ingest

#### 3. `kb-guide`

用途：

- 用户不知道该从哪看起
- 用户问“下一步读什么”“从哪个页面继续”
- 用户想围绕某个主题建立阅读路径或研究路径

核心职责：

- 给出最短阅读链
- 为每一页说明用途
- 指明读完后的下一步
- 必要时指出还缺什么资料

不负责：

- 深度内容讲解
- 直接写长篇研究结论

### 第二层：执行技能

#### 4. `kb-locate`

用途：

- 为其他 skill 提供稳定的页面定位过程

固定定位顺序：

1. `wiki/INDEX.md`
2. 相关 `wiki/concepts/`
3. 相关 `wiki/sources/`
4. 相关 `wiki/notes/`
5. 相关 `outputs/`
6. wiki 不足时才查 `raw/`

输出格式：

- 推荐主页面
- 次级参考页
- 建议阅读顺序

#### 5. `kb-explain-page`

用途：

- 围绕单页做细讲

固定输出结构：

- 这页在说什么
- 这页为什么重要
- 它和哪些页组成一条线
- 最容易误解什么
- 在真实研究或应用中怎么用
- 这页还缺什么

约束：

- 禁止只复述页面原文
- 必须补充页间关系和应用视角

#### 6. `kb-synthesize-output`

用途：

- 把一次高价值回答沉淀为产物或知识页更新

判断规则：

- 一次性问题但值得保留：写入 `outputs/`
- 可迁移的思考方式：写入 `wiki/notes/`
- 修正主题知识：更新 `wiki/concepts/`
- 只是短答且无复用价值：不落盘

附带动作：

- 更新 `wiki/INDEX.md`
- 更新 `wiki/log.md`

#### 7. `kb-route`

用途：

- 作为总路由器，判断请求应走哪条链

意图映射：

- “是什么 / 比较 / 总结 / 为什么” -> `kb-ask`
- “细讲 / 教我 / 怎么理解 / 怎么应用” -> `kb-teach`
- “从哪开始 / 先看什么 / 下一步” -> `kb-guide`
- “这个结果该不该存 / 写成产物” -> `kb-synthesize-output`

调用职责：

- 不直接长答
- 只负责判断工作流和下一步 skill

## 调用链设计

### 直接问答

`kb-route -> kb-ask -> kb-locate`

若结果有长期价值：

`kb-ask -> kb-synthesize-output`

### 教学讲解

`kb-route -> kb-teach -> kb-locate -> kb-explain-page`

若讲解中形成可迁移方法：

`kb-teach -> kb-synthesize-output`

### 研究导航

`kb-route -> kb-guide -> kb-locate`

必要时：

- 生成阅读顺序
- 指出缺失资料
- 指出后续应转入 `kb-ask` 还是 `kb-teach`

## 目录与放置建议

为 agent 额外增加一层操作资产，但保持极轻量：

```text
agent/
  skills/
    kb-ask/
    kb-teach/
    kb-guide/
    kb-locate/
    kb-explain-page/
    kb-synthesize-output/
    kb-route/
  playbooks/
    answer-template.md
    teach-template.md
    reading-path-template.md
    synthesis-template.md
  maps/
    topic-lines.md
    high-value-pages.md
    outputs-index.md
```

说明：

- `agent/skills/` 放各 skill 的 `SKILL.md`
- `agent/playbooks/` 放固定回答模板和输出格式
- `agent/maps/` 放为 agent 优化的轻量知识地图

这层是 agent 的操作层，不是用户主阅读层。

## 每个 Skill 的最小骨架

每个 `SKILL.md` 至少应包含：

### A. 何时触发

- 用户意图
- 关键词
- 与其他 skill 的边界

### B. 固定前置动作

- 是否必须先读 `wiki/INDEX.md`
- 是否必须先跑 `kb-locate`
- 是否必须优先查 `wiki/notes/`

### C. 执行步骤

- 读取顺序
- 判断分支
- 输出结构

### D. 禁止事项

- 不要从零综合
- 不要跳过 `wiki`
- 不要把讲解写成简单摘要
- 不要在无价值时滥写 `outputs/`

### E. 结束动作

- 是否更新 `outputs/`
- 是否更新 `wiki/notes/`
- 是否更新 `INDEX` / `log`

## 三个高频入口 Skill 的详细行为

### `kb-ask`

标准流程：

1. 读 `wiki/INDEX.md`
2. 调 `kb-locate`
3. 读核心 concept/source/output 页面
4. 生成回答
5. 区分：
   - wiki 已确认内容
   - 新补充的信息
   - 待验证推断
6. 如结果有长期价值，调用 `kb-synthesize-output`

默认回答风格：

- 先给结论
- 再给依据页
- 再指出知识空白

### `kb-teach`

标准流程：

1. 读 `wiki/INDEX.md`
2. 优先调 `kb-locate` 找 `wiki/notes/`
3. 若用户基于某个产物提问，先读对应 `outputs/`
4. 再补 concept/source 页面
5. 调 `kb-explain-page` 或按其模板输出

默认讲解结构：

1. 这页或这条线到底在解决什么问题
2. 它的核心断点是什么
3. 最容易混淆什么
4. 该如何思考、判断和应用
5. 还需要补什么证据

### `kb-guide`

标准流程：

1. 读 `wiki/INDEX.md`
2. 调 `kb-locate`
3. 选 1 到 3 页作为最短入口
4. 解释每页用途
5. 给出下一跳

默认输出结构：

- 先看什么
- 为什么先看
- 读完后去哪里
- 当前还缺什么

## `kb-synthesize-output` 的落盘规则

### 落到 `outputs/`

适用于：

- 对某个具体问题形成了完整答复
- 对某个阶段形成了阶段性 memo、报告、对比分析
- 未来高概率还会复用

### 落到 `wiki/notes/`

适用于：

- 形成了可迁移的判断框架
- 明确了某种研究直觉或应用方式
- 不只是回答当前问题，而是改变了以后怎么看类似问题

### 更新 `wiki/concepts/`

适用于：

- 新结论属于主题知识本身
- 新资料修正了旧判断
- 某个主题页明显缺关键链接或关键断点

## `agent/maps/` 的设计

虽然系统重点不是 tools，但仍建议给 agent 一层轻量导航材料：

### `topic-lines.md`

记录当前高价值主题线，例如：

- `RNN/LSTM -> attention -> Transformer -> systems`

用于让 agent 快速知道哪些页是同一研究链。

### `high-value-pages.md`

列出最值得优先看的页：

- 入口页
- 总导航页
- 关键概念页
- 关键默会知识页
- 关键输出页

### `outputs-index.md`

按问题类型列出已有产物，避免 agent 重复造轮子。

## 风险与边界

### 风险 1：skills 太多，实际不用

缓解：

- 高频只暴露 `kb-ask`、`kb-teach`、`kb-guide`
- 其他技能主要作为内部执行技能

### 风险 2：`kb-ask` 和 `kb-teach` 边界模糊

缓解：

- `ask` 追求回答
- `teach` 追求解释、误区、应用和思考路径

### 风险 3：所有请求都被写进 `outputs/`

缓解：

- 把 `kb-synthesize-output` 作为单独技能
- 明确“不落盘”也是允许的结果

### 风险 4：agent 仍然回到原始资料层从零综合

缓解：

- 每个 query/teach skill 都强制先读 `wiki/INDEX.md`
- 默认定位顺序固定为 `INDEX -> wiki -> outputs -> raw`

## 实施顺序

建议分三步落地：

### 阶段 1

先写 3 个入口 skill：

- `kb-ask`
- `kb-teach`
- `kb-guide`

### 阶段 2

再写 4 个执行 skill：

- `kb-locate`
- `kb-explain-page`
- `kb-synthesize-output`
- `kb-route`

### 阶段 3

补 `agent/playbooks/` 与 `agent/maps/`：

- 让 skill 输出更稳定
- 让 agent 更快知道该读什么

## 推荐结论

推荐采用 7-skill 双层结构，而不是极简三技能或大量细碎技能。

原因：

- 能同时覆盖问答、讲解、导航、沉淀四类高频任务
- 保持入口简单
- 给 agent 足够稳定的执行链
- 与当前仓库的 `raw / wiki / outputs` 三层结构和 `wiki/notes/` 默会知识层天然兼容

## 下一步

若此 spec 被接受，下一步应直接进入实现计划，内容包括：

- 创建 `agent/skills/` 目录结构
- 为 7 个 skill 编写 `SKILL.md`
- 创建 `agent/playbooks/` 模板
- 创建 `agent/maps/` 的初始导航文件
- 选 1 到 2 个真实主题做试运行验证
