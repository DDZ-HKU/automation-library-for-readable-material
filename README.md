# LLM Wiki

这是一个面向个人研究的本地知识库骨架，按最简单的三层结构组织：

- `raw/`：原始资料
- `wiki/`：由 LLM 持续维护的知识层
- `outputs/`：问答、报告、简报、比较分析等输出

核心思路不是“每次提问时再去原始文件里临时检索”，而是让 LLM 把知识持续编译进 wiki。原始资料保持不动，`wiki/` 持续更新，`AGENTS.md` 约束代理如何 ingest、query 和 lint。

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
   - 在 `wiki/sources/` 写摘要
   - 更新相关概念页和实体页
   - 更新 `wiki/INDEX.md`
   - 在 `wiki/log.md` 追加记录

### Query

1. 直接对 wiki 提问
2. 代理先读 `wiki/INDEX.md`
3. 代理读取相关页面并生成答案
4. 有长期价值的答案写入 `outputs/`，必要时再沉淀回 `wiki/`

### Lint

定期让代理巡检：

- 页面之间是否矛盾
- 是否有提到但没解释的主题
- 是否有缺少来源支撑的结论
- 是否有孤儿页
- 是否有应该补充的新资料方向

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
