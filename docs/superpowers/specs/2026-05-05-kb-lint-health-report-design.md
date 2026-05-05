# KB Lint Health Report Design

日期：2026-05-05

## 目标

为当前知识库增加一个可执行的 `scripts/kb lint` 能力，并同步固定其 Markdown 健康报告格式，使仓库里刚刚强化的 `Lint` 规则不只停留在文档层，而能生成稳定、可复用、可追踪的报告。

本次设计的目标是最小可落地版本：

- 扫描断链
- 扫描过期页面
- 扫描孤儿页
- 输出 Markdown 健康报告
- 不自动修复

## 非目标

- 不接外部 Confluence API
- 不扫描外网链接是否可访问
- 不自动修复页面
- 不在第一版构建全仓引用图数据库
- 不把 `raw/`、`marker/`、`docs/` 一并纳入健康检查

## 现状判断

当前仓库已经在入口层明确了 `Ingest / Query / Lint / Update` 四种模式，并对 `Lint` 给出了三类重点问题：

- 断链
- 超过 90 天未更新的高价值页面
- 孤儿页

但这些规则现在仍主要停留在：

- `AGENTS.md`
- `README.md`
- `wiki/notes/workflows/how-to-run-ingest-query-lint-update-in-this-repo.md`

也就是说，规则已经存在，但缺一个机械执行面。当前最合适的承载点是现有的 `scripts/kb`，因为它已经是知识库检索的统一入口，职责上接近一个轻量 facade。

## 设计原则

### 1. 入口单一

不新增第二套脚本名，直接扩展 `scripts/kb`，加入 `lint` 子命令。

### 2. 先报告，后修复

第一版只生成 health report，不做任何自动修改，符合当前仓库“修复前先告知”的规则。

### 3. 本地知识库优先

第一版只检查本地可解析目标，聚焦：

- `wiki/`
- `outputs/`
- `wiki/INDEX.md`

不把外网可用性检测混进来。

### 4. 规则可解释

每类问题都要输出“为什么被判为问题”，而不是只给文件名列表。

### 5. 定义从轻

孤儿页第一版采用“未登记在 `wiki/INDEX.md`”这个明确定义，而不是一上来引入复杂的入链分析。

## 用户接口

新增命令：

```bash
scripts/kb lint
```

默认行为：

- 扫描当前仓库内的 `wiki/` 与 `outputs/`
- 生成一份新的 Markdown 健康报告
- 把报告写到 `outputs/`
- 同时在终端打印摘要与输出路径

默认输出文件名：

```text
outputs/wiki-health-report-YYYY-MM-DD.md
```

如果同一天重复生成，允许覆盖同名报告。第一版不做带序号的多版本输出。

## 检查范围

### 1. 断链检查

检查来源：

- `wiki/INDEX.md`
- `wiki/` 下所有 Markdown 页面
- `outputs/` 下所有 Markdown 页面

检查对象：

- Markdown 相对链接
- 指向本仓库文件的绝对本地链接
- `[[slug]]` 形式的 wiki-link

第一版规则：

- 只检查能映射到仓库内 Markdown 页面的目标
- 忽略外部 `http/https` 链接
- 忽略锚点本身是否存在，只先判断目标文件是否存在

输出字段：

- 引用页
- 引用文本或目标
- 解析后的目标路径
- 问题类型：`missing-target`

### 2. 过期检查

检查范围：

- `wiki/` 下所有 Markdown 页面

第一版判定规则：

- 页面中存在 `updated: YYYY-MM-DD`
- 距当前日期超过 90 天

第一版不额外判断“是否高频引用”，因为那需要引入更复杂的权重规则。先把“超过 90 天”作为硬阈值报告出来，再由人决定是否真要更新。

输出字段：

- 页面路径
- `updated` 日期
- 距今天的天数
- 问题类型：`stale-page`

### 3. 孤儿页检查

检查范围：

- `wiki/` 下所有 Markdown 页面

第一版判定规则：

- 页面存在
- 但其相对路径未出现在 `wiki/INDEX.md`

明确例外：

- `wiki/INDEX.md`
- `wiki/log.md`
- `wiki/overview.md`

输出字段：

- 页面路径
- 所属目录
- 问题类型：`orphan-page`
- 建议挂载位置

## 报告格式

报告写成稳定 Markdown，结构固定如下：

```md
# Wiki Health Report

日期：YYYY-MM-DD

## Summary

- broken links: N
- stale pages: N
- orphan pages: N
- report scope: wiki/, outputs/

## Broken Links

## Stale Pages

## Orphan Pages

## Suggested Fixes

## Scope Notes
```

各节要求：

- `Summary`：给出总数和范围
- `Broken Links`：逐条列出断链
- `Stale Pages`：列出页面与过期天数
- `Orphan Pages`：列出页面与建议挂载位置
- `Suggested Fixes`：按问题类型给出人工处理建议
- `Scope Notes`：声明本次未覆盖外网检查、未验证锚点、未自动修复

如果某一类问题为空，也保留标题，并写：

```md
无
```

## 实现位置

修改现有文件：

- `scripts/kb`

不新增独立脚本。理由：

- 现有 `scripts/kb` 已是知识检索 facade
- `lint` 是同一层级的知识库维护操作
- 避免把知识库入口拆散成多个平行脚本

## 实现思路

### 1. 扫描文件集合

收集：

- `wiki/**/*.md`
- `outputs/**/*.md`

并分别构造：

- 全部 wiki 页面清单
- 全部 outputs 页面清单
- `wiki/INDEX.md` 中已登记页面集合

### 2. 提取链接

从 Markdown 文本中提取：

- `[label](target)`
- `[[slug]]`

对 target 做归一化：

- 相对路径转仓库绝对路径
- 去掉锚点部分
- 只保留文件路径判断

### 3. 判断断链

若目标属于仓库内 Markdown 文件但不存在，则记为断链。

### 4. 判断过期

解析 `updated:` 字段，与当前日期比较，超过 90 天则记为过期。

### 5. 判断孤儿页

若页面不在 `wiki/INDEX.md` 中，且不是核心例外页，则记为孤儿页。

### 6. 生成报告

把三类结果渲染成 Markdown，写入 `outputs/wiki-health-report-YYYY-MM-DD.md`。

### 7. 终端摘要

命令结束时打印：

- 各类问题计数
- 报告输出路径

## 错误处理

- 如果 `rg` 不存在，保持与现有 `scripts/kb` 一致，直接报错退出
- 如果报告文件无法写入，返回非零退出码
- 如果某页没有 `updated:`，不视为脚本错误，只是不参与“过期”判断
- 如果某个链接格式无法完全解析，第一版忽略，不阻断整个 lint

## 测试与验证

最小验证方式：

1. 运行 `scripts/kb lint`
2. 确认生成 `outputs/wiki-health-report-YYYY-MM-DD.md`
3. 人工检查报告是否包含：
   - 至少一类问题的统计
   - 固定章节结构
4. 若仓库当前恰好无某类问题，确认对应章节显示 `无`

附加验证：

- 人工制造一个临时断链，确认会被报告
- 人工检查 1 个超过 90 天未更新页面是否进入 `Stale Pages`
- 人工检查新建未登记页是否进入 `Orphan Pages`

## 方案比较

### 方案 A：直接在 `scripts/kb` 里实现 `lint`

优点：

- 改动小
- 用户入口清晰
- 与现有搜索命令同层

缺点：

- 脚本会继续变长

### 方案 B：新建独立 `scripts/kb-lint`

优点：

- 文件职责更单一

缺点：

- 入口分裂
- 与现有 `scripts/kb` facade 不一致

### 方案 C：先只写报告模板，不写脚本

优点：

- 风险最低

缺点：

- 仍停留在手工执行层
- 不能满足“开始把约束变成可执行”的目标

推荐方案：

- 采用方案 A

理由：

- 这是当前最小、最一致、最符合仓库现有工具层结构的实现方式

## 风险与后续扩展

第一版有意保留的缺口：

- 不检查外部链接是否存活
- 不检查锚点是否失效
- 不做“被引用权重”分析
- 不自动修复

后续可以演进的方向：

- `scripts/kb lint --stdout`
- `scripts/kb lint --write <path>`
- 更严格的孤儿定义：结合入链图
- 更细的过期规则：只报告高价值页
- health report 自动回写 `wiki/log.md`

## 结论

本次实现应聚焦一个明确交付物：

- `scripts/kb lint`
- 固定格式的 `outputs/wiki-health-report-YYYY-MM-DD.md`

这样可以先把 `Lint` 从规则升级为可执行能力，同时保持范围小、语义清晰、对现有仓库侵入低。
