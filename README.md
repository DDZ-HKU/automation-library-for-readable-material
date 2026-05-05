# LLM Wiki

这是一个面向个人研究的本地知识库骨架，按最简单的三层结构组织：

- `raw/`：原始资料
- `wiki/`：由 LLM 持续维护的知识层
- `outputs/`：问答、报告、简报、比较分析等输出

核心思路不是“每次提问时再去原始文件里临时检索”，而是让 LLM 把知识持续编译进 wiki。原始资料保持不动，`wiki/` 持续更新，`AGENTS.md` 约束代理如何 ingest、query、lint 和 update。

更细的查询路由、升格判断、规则分类和 `ops` 适用边界，统一下沉到 `wiki/notes/workflows/`，这里不再重复展开。

现在这个仓库除了维护显性知识外，还增加了一层“默会知识解读”：

- `wiki/sources/` 记录资料明确说了什么
- `wiki/concepts/` 记录当前已确认的主题知识
- `wiki/notes/` 记录判断框架、研究脉络、应用方法和隐含前提
- `outputs/` 保存面向具体问题的报告、总结和阶段性成果

## 目录结构

```text
.
├── AGENTS.md
├── README.md
├── outputs/
├── raw/
├── templates/
└── wiki/
```

当前仓库在保持三层结构简单的同时，`wiki/` 内部预留了少量子目录，方便后续增长：

- `wiki/INDEX.md`：wiki 内容索引入口
- `wiki/log.md`：时间日志
- `wiki/overview.md`：整体概览
- `wiki/concepts/`：主题和概念
- `wiki/entities/`：人物、组织、产品、术语
- `wiki/sources/`：单篇原始资料的摘要页
- `wiki/notes/`：阶段性分析、问答沉淀与默会知识解读

其中 `wiki/notes/` 进一步按职责分成：

- `wiki/notes/workflows/`：工作流和操作约定
- `wiki/notes/frameworks/`：通用思考框架与阅读模板
- `wiki/notes/cases/`：围绕具体主题写成的默会知识案例

## 三个文件夹怎么用

### `raw/`

把文章、笔记、截图、PDF、网页剪藏、会议记录直接扔进去。不要先整理，也不要先手工改名。LLM 的任务就是从混乱原料里提炼结构。

### `wiki/`

你尽量不要手写这里的内容。这个目录是 LLM 的工作区，用来维护主题页、摘要页、关联页、索引、交叉链接，以及更高层的默会知识解读。

### `outputs/`

这里放最终产物，例如：

- 问题答案
- 阶段研究报告
- 对比分析
- 简报草稿
- 可以回灌到 wiki 的阶段性结论

## 推荐工作流

### Ingest

1. 把文件放进 `raw/`
2. 告诉代理处理这些资料
3. 代理读取资料后：
   - 去重、结构化、精确化，而不是搬运原文
   - 在 `wiki/sources/` 写摘要
   - 将分散原始页面提炼成更稳定的话题页
   - 更新相关概念页和实体页
   - 更新 `wiki/INDEX.md`
   - 在 `wiki/log.md` 追加记录

如果上游来自 Confluence、网页剪藏或其他文档系统，也按同一规则处理：原文留在 `raw/`，提炼结果进入 `wiki/`。

### Query

1. 直接对 wiki 提问
2. 代理先读 `wiki/INDEX.md`
3. 代理并发检索：
   - 已合成的 `wiki/` / `outputs/`
   - 必要时对应的 `raw/` 原始资料
4. 优先使用已合成知识回答，原始资料只做补充和校对
5. 每条关键信息尽量带来源
6. 有长期价值的答案写入 `outputs/`，必要时再沉淀回 `wiki/`

### Lint

定期让代理巡检：

- 来源或交叉引用是否断链
- 高价值页面是否超过 90 天未更新
- 是否有未登记到目录的孤儿页
- 页面之间是否矛盾
- 是否有提到但没解释的主题
- 是否有缺少来源支撑的结论
- 是否有应该补充的新资料方向

lint 的默认产物应先是一份健康报告；是否自动修复，应在修复前明确告知。

当前可执行入口：

- `scripts/kb lint`
- 默认输出到 `outputs/wiki-health-report-YYYY-MM-DD.md`

### Update

发现新内容后，不要默认另起一页，而是优先合并进已有话题页：

- 保留原有准确内容
- 只替换过时部分
- 补充新的来源与修订说明
- 递增版本或保留可追踪的变更历史
- 同步更新 `wiki/INDEX.md` 和 `wiki/log.md`

## 最小使用示例

你现在就可以直接这样用：

- “读取 `raw/` 里的所有内容，按 `AGENTS.md` 规则在 `wiki/` 中编译一个 wiki。”
- “基于 `wiki/` 中所有内容，给我写一份 500 字简报，保存到 `outputs/`。”
- “审查整个 `wiki/`，列出矛盾、缺失主题和没有来源支持的声明。”

## 下一步建议

最合适的下一步是：

1. 先放入 3 到 5 份真实资料到 `raw/`
2. 让我做第一轮 ingest
3. 再根据你的真实使用方式微调 `AGENTS.md`

## PDF to Markdown

这个工作区使用本地 `marker/` 工具先把 PDF 转成 Markdown，再进入知识库 ingest 流程。

基本流程：

1. 把 PDF 放进 `raw/inbox/`
2. 运行 `scripts/pdf-to-md raw/inbox/<file>.pdf`
3. 确认 Markdown 出现在 `raw/sources/`
4. 再把新的 Markdown 按 `AGENTS.md` 规则 ingest 到 `wiki/`
