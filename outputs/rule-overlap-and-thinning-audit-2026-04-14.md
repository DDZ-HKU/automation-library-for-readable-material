# 规则重叠与减重审计

日期：2026-04-14

## 这份 audit 在做什么

随着新的 workflow guides 增加，当前仓库的规则已经分布在多个层级：

- `AGENTS.md`
- `README.md`
- `.codex/skills/kb-wiki-first/SKILL.md`
- `wiki/notes/workflows/*`

这会带来一个新问题：

- 哪些规则应留在入口层
- 哪些规则应只留在 guide 层
- 哪些地方已经开始重复

这份 audit 的目标，就是对这些规则做一次“减重”视角的盘点，而不是继续新增规则。

## 盘点对象

本次重点检查：

- [AGENTS.md](/Users/ddz/Documents/exp/AGENTS.md)
- [README.md](/Users/ddz/Documents/exp/README.md)
- [.codex/skills/kb-wiki-first/SKILL.md](/Users/ddz/Documents/exp/.codex/skills/kb-wiki-first/SKILL.md)
- [how-to-route-knowledge-queries-in-this-repo.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-route-knowledge-queries-in-this-repo.md)
- [how-to-manage-partially-promoted-outputs.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-manage-partially-promoted-outputs.md)
- [how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md)
- [how-to-apply-ops-protocol-outside-autonomous-runs.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-apply-ops-protocol-outside-autonomous-runs.md)

## 一、哪些规则应留在入口层

入口层包括：

- `AGENTS.md`
- `README.md`
- `kb-wiki-first`

这些文件最适合承载的，不是细节，而是：

### 1. 仓库身份与总目标

应留在：

- `AGENTS.md`
- `README.md`

包括：

- 仓库是 LLM 维护的知识库
- 三层结构：`raw / wiki / outputs`
- `wiki/notes/` 是 tacit knowledge 层

### 2. 默认总顺序

应留在：

- `AGENTS.md`
- `kb-wiki-first`

包括：

- 非平凡 query 先看 `wiki/INDEX.md`
- 优先用 wiki，不足时再回 `raw`
- 结果有长期价值时保存到 `outputs`

### 3. 最小工作协议

应留在：

- `AGENTS.md`

包括：

- ingest / query / lint 的基本职责
- source traceability
- 冲突时不静默覆盖

## 二、哪些规则应下沉到 guide 层

下面这些已经不适合继续留在入口层反复出现，而应主要由 guide 承担：

### 1. 查询路由细节

例如：

- `notes` 和 `outputs` 谁优先
- `frameworks` 和 `cases` 谁优先
- 什么情况下才回 `raw`

应主要留在：

- [how-to-route-knowledge-queries-in-this-repo.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-route-knowledge-queries-in-this-repo.md)

### 2. 部分升格管理细节

例如：

- 什么算 `partially promoted`
- 什么时候补 `Source Trace`
- output 与 wiki 页如何双向回链

应主要留在：

- [how-to-manage-partially-promoted-outputs.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-manage-partially-promoted-outputs.md)

### 3. 规则对象分类细节

例如：

- `guide / sensor / facade / protocol` 的边界

应主要留在：

- [how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md)

### 4. ops 外溢边界

例如：

- full ops protocol 与 general quality rules 的区别

应主要留在：

- [how-to-apply-ops-protocol-outside-autonomous-runs.md](/Users/ddz/Documents/exp/wiki/notes/workflows/how-to-apply-ops-protocol-outside-autonomous-runs.md)

## 三、当前最明显的重叠

### 重叠 1：`AGENTS.md` 与 `kb-wiki-first`

重复点：

- 先看 `INDEX`
- 优先用 `wiki`
- `raw` 只在不足时回查

判断：

- 不构成冲突
- 但属于“入口层双写”

建议：

- `AGENTS.md` 保留原则性表述
- `kb-wiki-first` 保留执行顺序与工具入口
- 不再把更细路由规则回写到两边

### 重叠 2：`AGENTS.md` 与 query routing guide

重复点：

- 先看 wiki
- 何时回 raw

判断：

- 当前还能接受
- 但如果继续把路由细节加回 `AGENTS.md`，就会开始冗余

建议：

- `AGENTS.md` 只保留总原则
- 所有“怎么选 notes / outputs / cases / frameworks”的细节只写在 guide

### 重叠 3：`README.md` 与 `AGENTS.md`

重复点：

- 三层结构
- ingest / query / lint 基本工作流

判断：

- 这是合理重复
- 因为 README 给人看，AGENTS 给代理看

建议：

- 保留
- 但不要让 README 承载过多规则细节

## 四、当前最值得减重的地方

### 1. 不要再把新 guide 细节补回 `AGENTS.md`

当前最需要的不是给 `AGENTS.md` 加更多细节，而是守住它作为总协议入口的角色。

### 2. `README.md` 不要升级成第二份 AGENTS

README 适合保留：

- 仓库用途
- 基本目录
- 基本工作流

不适合承载：

- 细粒度路由规则
- 升格边界
- protocol 分类法

### 3. `kb-wiki-first` 只保留最小查询顺序

如果把更多路由分支继续塞进 skill，会开始和 guides 重叠。

更稳的做法是：

- skill 只保留默认顺序和最低限度约束
- 细节交给 workflow guides

## 五、推荐的结构边界

最稳的分层应是：

### `README.md`

负责：

- 仓库是什么
- 基本怎么用

### `AGENTS.md`

负责：

- 总体协议
- ingest / query / lint 原则
- source traceability 与冲突处理

### skills

负责：

- 默认路由
- 最小执行顺序
- 工具入口

### workflow guides

负责：

- 具体情景下的详细规则
- 例外边界
- 决策树

## 六、下一步建议

如果要真的减重，最值得做的不是立刻改一堆文件，而是先遵守一个原则：

**以后新增规则时，先决定它属于入口原则、skill 最小约束，还是 guide 细节；不要默认所有地方都补一遍。**

之后若要真改文件，建议先从最轻的动作开始：

1. 给 `README.md` 明确“更细规则见 workflow guides”
2. 给 `AGENTS.md` 保持原则性，不再加细分路由
3. 给 `kb-wiki-first` 保持最小顺序，不继续加分支

## 一句话总结

当前仓库的主要问题不是规则太少，而是：

**规则已经够多了，接下来最重要的是守住分层，不让入口层重新长回一堆细则。**
