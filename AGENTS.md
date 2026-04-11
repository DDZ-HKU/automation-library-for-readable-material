# AGENTS

本仓库是一个由 LLM 维护的个人知识库。你的职责不是做一次性问答，而是把 `raw/` 中的原始资料持续编译成 `wiki/`，并把高价值输出沉淀到 `outputs/`。除了显性知识整理外，还要在 `wiki/notes/` 中持续沉淀可复用的“默会知识解读”。

## Mission

在不修改原始资料的前提下，把新资料整合进 `wiki/`。回答问题时优先复用已有 wiki，而不是每次从零综合。必要时把答案保存为 `outputs/` 中的独立产物。对长期有价值的判断框架、研究直觉、应用方法和思考路径，应进一步沉淀为 `wiki/notes/` 中的默会知识页。

## Repository Contract

### `raw/`

原始资料层。

- 可以读取
- 可以新增文件
- 不要改写已有原始资料内容
- 不要要求用户先整理、重命名或清洗
- 允许目录处于“混乱但可读”的状态

### `wiki/`

知识层，由 LLM 维护。

- 允许创建、重写、合并、拆分页
- 允许补充摘要、交叉链接和修订说明
- 允许基于新证据修正旧结论
- 允许在 `wiki/notes/` 中沉淀默会知识、判断框架和研究脉络
- 用户原则上只阅读，不手工维护

### `outputs/`

输出层，用于保存：

- 报告
- 简报
- 对比分析
- 问题答案
- 需要保留的阶段性研究成果

## Wiki Rules

### Page structure

- 每个主要主题在 `wiki/` 中应有自己的 Markdown 页面
- 每个 wiki 页面都应以简短摘要开头
- 页面中优先使用 `[[topic-name]]` 风格表达相关主题
- 若当前环境或文件体系不支持 wiki-link，也可补充普通 Markdown 链接
- 对 `wiki/notes/` 中的默会知识页，应显式区分：
  - 已确认的显性知识
  - 默会知识解读
  - 尚待验证的推断

### Required files

- `wiki/INDEX.md`：列出主要页面及一行说明
- `wiki/log.md`：追加式时间日志
- `wiki/overview.md`：当前知识范围与状态

### Internal organization

允许使用子目录维持可读性，例如：

- `wiki/concepts/`
- `wiki/entities/`
- `wiki/sources/`
- `wiki/notes/`

当 `wiki/notes/` 增长后，优先按职责进一步细分：

- `wiki/notes/workflows/`：可重复执行的工作流与操作约定
- `wiki/notes/frameworks/`：通用判断框架、阅读模板、方法论
- `wiki/notes/cases/`：围绕某一主题线的默会知识案例页

但要保持整体简单，不引入数据库或复杂基础设施。

### Tacit knowledge layer

`wiki/notes/` 不只是临时笔记区，也是本仓库的“默会知识层”。这里用于保存：

- 判断框架
- 研究脉络
- 应用方法
- 阅读论文时未被直接说出的隐含前提
- 对已有主题的可迁移思考方式

目录约定：

- `frameworks/` 放可跨主题复用的模板
- `cases/` 放基于已有知识线写成的案例解读
- `workflows/` 放知识库自身的操作流程与工作习惯

默会知识页不应简单重复 `wiki/sources/` 或 `wiki/concepts/` 的摘要，而应回答：

- 这些材料真正教会了我们什么思考方式
- 应该如何判断类似问题
- 这些知识在真实研究或应用中如何使用

## Operating Rules

### Before answering any non-trivial question

1. 先读 `wiki/INDEX.md`
2. 定位相关页面
3. 优先基于已有 wiki 回答
4. 如 wiki 不足，再回到 `raw/` 查原始资料
5. 明确区分：
   - wiki 已确认内容
   - 新资料带来的新增信息
   - 尚未验证的推断
6. 如果问题要求更高层的理解、判断或应用，优先查找相关 `wiki/notes/` 中的默会知识页

### During ingest

处理新资料时按以下顺序执行：

1. 识别资料类型、主题、日期、作者、来源
2. 提取核心论点、事实、定义、争议和关键数据
3. 在 `wiki/sources/` 新建或更新资料摘要页
4. 更新相关主题页、概念页、实体页和 `wiki/overview.md`
5. 用 `[[topic-name]]` 或普通链接补充交叉引用
6. 如发现冲突，显式写出“新资料与旧结论的冲突”
7. 更新 `wiki/INDEX.md`
8. 在 `wiki/log.md` 追加记录

若新资料使某个主题的判断框架、研究直觉或应用方法发生了实质推进，应额外更新相关 `wiki/notes/` 默会知识页。

### During query

如果用户的问题产生了长期有价值的结果：

1. 先回答用户问题
2. 将结果保存到 `outputs/`
3. 如该结果应成为知识库长期组成部分，再同步沉淀到 `wiki/notes/`
4. 更新 `wiki/INDEX.md` 和 `wiki/log.md`

如果用户明确要求“教会我如何思考、判断和应用”，默认不仅要给答案，还应优先产出或更新对应的默会知识页。

### During lint

每次 lint 至少检查：

- 页面之间的矛盾
- 提到但未解释的主题
- 缺来源支撑的结论
- 孤儿页
- 高价值但尚未建页的概念
- 已被新资料部分推翻但未修正的页面
- 可以补洞的潜在新资料方向

## Writing Conventions

### File naming

- 文件名用 kebab-case
- 简洁且语义清楚
- 不要频繁重命名

### Link style

- 页面正文优先使用 `[[topic-name]]`
- 如需确保跨工具兼容，可同时保留普通 Markdown 链接
- 新增重要页面后，尽量从至少一个已有页面链接到它

### Source traceability

- 重要事实尽量标出来自哪份资料或哪份资料摘要页
- 不确定的结论标记为“待验证”或“推断”
- 不要静默覆盖被新资料挑战的旧说法
- 默会知识页中的判断应尽量指回相关概念页或来源页，避免与显性知识脱节

### Editing style

- 优先增量更新，不做无意义大重写
- 页面过宽时拆页
- 页面高度重复时合并

## Required Formats

### `wiki/INDEX.md`

按类别列出页面，至少包含：

- 页面名
- 一句话说明
- 最近更新日期
- 关联来源数（如适用）

### `wiki/log.md`

每条记录以如下格式开始：

```md
## [YYYY-MM-DD] type | title
```

其中 `type` 通常是：

- `ingest`
- `query`
- `lint`
- `refactor`

## Decision Policy

面对信息冲突时：

1. 不要假装一致
2. 标出冲突双方
3. 优先信任更直接、更近的原始资料
4. 无法判断时保留“待验证”

## First Read Priority

开启新会话时，优先阅读：

1. `README.md`
2. `wiki/INDEX.md`
3. `wiki/overview.md`
4. `wiki/log.md`

然后再根据任务读取相关页面和原始资料。
