# 从 Tool 论文到 CLI 工具体系：怎么把工程真正搭起来

日期：2026-04-13

## 结论

如果你在另一个项目里已经有很多 CLI，可优化的重点不是“再多加几个命令”，而是把系统拆成 5 层：

1. `tool corpus`
2. `retriever`
3. `planner`
4. `executor`
5. `tool asset layer`

这些论文真正给你的，不是抽象概念，而是这 5 层分别该怎么建：

- `ToolLLM`：教你搭 `tool corpus + retriever + planner + evaluator`
- `CREATOR`：教你把 `planner` 再拆成 `creation / decision / execution / rectification`
- `LATM`：教你把 `tool creation` 和 `tool usage` 拆成高低成本双层
- `ToolLibGen`：教你给大量工具增加 `clustering / aggregation / review`
- `API Synthesis`：教你在某些场景里直接从 examples 合成实现，而不是一直靠检索现有工具

如果把这些落到 CLI 项目里，最合理的目标不是：

- “agent 会调很多命令”

而是：

- “agent 能从很多 CLI 中稳定找对、排对、调对，并让工具资产随着使用不断演化”

如果进一步落到当前这个知识库仓库，最重要的还不是“脚本系统怎么扩”，而是：

- 如何把 `raw -> wiki -> outputs` 的内容流
- 和 `atomic -> facade -> planning -> governance` 的工具流

并行组织成一个可持续维护的 agentic knowledge base。

## 一、逐篇看：它们在工程上到底怎么搭

### 1. ToolLLM

ToolLLM 的系统不是一个 prompt，而是五个部件：

- `ToolBench`
  - 大规模真实 API 语料库
- `ToolLLaMA`
  - 训练后的 tool-use 模型
- `API retriever`
  - 先从大量 API 里缩小候选空间
- `DFSDT`
  - 用搜索式推理而不是单路径 ReAct
- `ToolEval`
  - 用自动 pass/win 指标评估结果

把它翻译成 CLI 世界，就是：

- 你需要一个**工具语料层**
  - 所有 CLI 的名称、用途、输入、输出、副作用、类别
- 你需要一个**检索层**
  - 先把可能相关的 CLI 缩小到 3 到 10 个
- 你需要一个**规划层**
  - 在候选工具里排顺序和回退
- 你需要一个**评估层**
  - 判断这次 CLI 调用链是否真的完成任务

ToolLLM 最值得借鉴的技术点：

- 不把 tool use 当单步动作
- 检索先行
- 多路径规划
- 自动评估不可少

### 2. CREATOR

CREATOR 的核心不是“工具更多”，而是把 agent 推理拆成 4 个显式阶段：

- `Creation`
- `Decision`
- `Execution`
- `Rectification`

这意味着什么：

- 不要让同一个步骤同时承担
  - 抽象出可复用方法
  - 决定当前怎么调用
  - 真正执行
  - 修错误

在 CLI 项目里，这一层很重要：

- `Creation`
  - 从经常重复的原子 CLI 组合里提炼新脚本
- `Decision`
  - 当前任务该选哪个脚本/命令
- `Execution`
  - 真的运行命令
- `Rectification`
  - 如果失败，是修参数、换命令，还是升级成新脚本

CREATOR 最值得借鉴的技术点：

- 把“造工具”和“用工具”彻底解耦
- 给失败留 rectification 环节
- 用代码作为可检查的中介，而不是只靠自然语言思考

### 3. LATM

LATM 的关键不是认知拆分，而是成本拆分：

- `tool maker`
- `tool user`

并且它把工具复用理解成：

- `functional cache`

这在 CLI 项目里对应得非常直接：

- 高能力 agent：
  - 观察长期重复模式
  - 把原子 CLI 组合升格成项目脚本
- 低成本 agent：
  - 日常只调这些脚本

这会带来两个效果：

- 平均推理成本下降
- 任务稳定性上升

LATM 最值得借鉴的技术点：

- maker / user 分层
- 一次性造工具，多次复用
- 缓存“功能”而不是缓存“答案”

### 4. ToolLibGen

ToolLibGen 的问题比前面又高一层：

- 工具会造了
- 工具会用了
- 但工具开始太多了

它的解决方式是：

- `tool clustering`
- `tool aggregation`
- `code agent + reviewing agent`

也就是：

1. 先按功能把工具分组
2. 再在每组里抽共享逻辑
3. 合并成更少但更泛化的工具
4. 用 review agent 确认功能没丢

翻译到 CLI 项目里，就是：

- 你的 `scripts/` 不能一直平铺
- 要开始按功能做：
  - search
  - verify
  - ingest
  - run-control
  - deploy
- 同类脚本开始多时，要合并和抽公共逻辑

ToolLibGen 最值得借鉴的技术点：

- 聚类不是为了好看，是为了降低 retrieval ambiguity
- 聚合不是为了减少文件数，而是为了提高“检索到的工具真的有用”的概率
- 需要 review 闭环，不然合并后容易丢能力

### 5. API Synthesis Using LLMs

这篇不在主线正中央，但对你也很重要。

它告诉你：

- 有些时候不该一直从现有工具库里找
- 而是应该直接综合一个新的实现

它的系统关键点是：

- 输入输出示例
- API signature
- assistant context
- few-shot
- follow-up prompts
- compile / test / readability 验证

放到 CLI 世界里，这意味着：

- 如果现有 CLI 都不合适
- 又已经能明确输入输出行为

那就可以直接让高能力 agent：

- 写一个新脚本
- 跑测试
- 失败后 follow-up 修复

也就是从“检索现有工具”切换到“合成新工具”。

## 二、你在 CLI 项目里最应该照抄的结构

### 1. 工具语料层

不要只有一堆脚本文件。

至少要给每个 CLI 建立这些元信息：

- name
- purpose
- category
- inputs
- outputs
- side effects
- examples
- risk level

这就是 CLI 版的 ToolBench。

没有这一层，后面的检索和规划会很差。

### 2. 检索层

在很多 CLI 里直接选命令，agent 会不稳。

应该先做一个 retriever：

- 关键词检索
- 标签检索
- 类别检索
- 相似工具排序

这就是 CLI 版的 API retriever。

最简单做法：

- 一个 `tools-index.json` 或 `tools-index.yaml`
- 一个 `scripts/tool-search`

### 3. 规划层

不要让 agent 一次性自由想完整路径。

更稳的是：

- 先选候选工具
- 再排 1 到 3 步最小链路
- 如果失败能回退

如果工具特别多，就上 ToolLLM 那种：

- search-based planning
- 多候选路径比较

### 4. 执行层

执行层应只做一件事：

- 跑命令

不要把：

## 三、把这套结构映射到当前知识库

如果按当前仓库的实际结构来映射，这 5 层可以进一步压缩成 4 个对知识库更有用的层：

1. `atomic`
2. `facade`
3. `planning`
4. `governance`

原因很简单：

- `tool corpus + retriever + executor` 在知识库里并不是完全分离的独立产品层
- 它们更常体现为“底层命令 + 中层脚本 + 技能路由 + ops 协议”的组合

### 1. Atomic Layer

当前仓库里就是：

- `rg`
- `sed`
- `ls`
- `git status`
- `pytest`

这一层的角色不是主工作流，而是保底原语。

### 2. Facade Layer

当前最典型的是：

- `scripts/kb`
- `scripts/pdf-to-md`

这一层真正解决的问题不是“少打一串命令”，而是：

- 降低知识任务的检索歧义
- 稳定输入输出
- 让 agent 更容易学会什么时候该调用什么

### 3. Planning Layer

当前对应的是：

- `kb-wiki-first`
- `kb-route`
- `kb-ask`
- `kb-teach`
- `kb-explain-page`
- `kb-autonomous-run`

这一层承担的不是执行，而是：

- 先读哪里
- 如何区分 confirmed / tacit / inference
- 什么时候回到 `raw/`
- 什么时候把结果留在 `outputs/`
- 什么时候进一步沉淀到 `wiki/notes/`

### 4. Governance Layer

当前对应的是：

- `ops/workboard.md`
- `ops/runbook.md`
- `ops/handoff.md`
- continuation scripts

这一层决定的不是“如何调用命令”，而是：

- 什么时候继续执行
- 什么时候必须验证
- 什么时候可以 handoff
- 什么时候需要人类决策

这意味着：当前知识库已经不只是内容仓库，也已经是一个带运行协议的 agent system。

## 四、这对知识库设计意味着什么

如果你要更新这个知识库设计，优先级不该是“多加几个 script”，而应该是下面这个判断顺序：

### 情况 A：agent 只是偶尔缺一个底层动作

先补 atomic 能力，不要急着设计新协议。

### 情况 B：同类知识任务反复出现

优先升格成 facade。

比如：

- 搜 wiki
- 查 output
- 找 related pages
- 预处理 PDF

### 情况 C：facade 已存在，但 agent 还是经常读错页、走错顺序、沉淀错层

这不是脚本缺失，而是 planning 问题。

应该优先更新：

- `kb-route`
- `kb-teach`
- `kb-guide`
- `kb-synthesize-output`

### 情况 D：agent 完成、验证、停机、handoff 经常不稳

这也不是多写一个脚本就能解决，而是 governance 问题。

应该优先更新：

- `ops/runbook.md`
- `ops/workboard.md`
- `ops/handoff.md`
- continuation scripts

### 情况 E：某个 output 已经提炼出长期稳定的判断模板

这时不应只让它留在 `outputs/`，而应升级到：

- `wiki/notes/frameworks/`

如果它讲的是可重复执行流程，则升级到：

- `wiki/notes/workflows/`

## 五、对当前仓库最实际的下一步

基于这次映射，当前仓库最实际的设计推进不是重写全部脚本，而是：

1. 给 repo-local tools 增加更清楚的元信息层
2. 明确 outputs 升格为 framework / workflow 的判断规则
3. 继续把知识任务的高频错误优先归因为 facade、planning 还是 governance 问题，而不是笼统归因为“agent 不够聪明”

## 六、一句话总结

对普通 CLI 项目，这些论文教你搭的是多层工具系统。

对当前知识库，这些论文进一步教你的，是：

**不仅要维护内容层，还要维护一个能让 agent 稳定提取、组织、验证和交接知识的工具治理层。**

## Source Trace

这份 output 的核心设计判断，已部分回灌到以下 wiki 页面：

- [how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)

这份 output 仍保留的独特价值是：

- 面向一般 CLI 项目的五层系统映射
- 面向当前知识库仓库的具体落地展开
- 比 framework 更长的应用级说明

## 关联页面

- [../wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)
- [../outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md](/Users/ddz/Documents/exp/outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md)

- 选命令
- 解释原因
- 修错误

都混在执行层里。

### 5. 校验层

这是大多数系统最缺的一层。

每个重要 CLI / facade 都要有：

- 成功条件
- 失败条件
- 可机器判断的 verification

否则 agent 看起来很会做事，实际上只是很会生成状态说明。

### 6. 资产层

当脚本数量多起来后，要有资产治理：

- clustering
- aggregation
- review
- deprecation

这就是 ToolLibGen 最直接的启发。

## 三、如何把这些论文落到你当前另一个项目

### Phase 1: 原子 CLI 清点

输出一个总表：

- 命令名
- 用途
- 输入
- 输出
- 副作用

### Phase 2: 提升成 task facades

把高频重复组合变成脚本。

例如：

- `search-*`
- `verify-*`
- `build-*`
- `ops-*`

### Phase 3: 加 retriever

让 agent 先检索 facades，再决定调用。

### Phase 4: 加 maker-user 分层

- 高能力 agent 负责造脚本
- 常规 agent 只负责用脚本

### Phase 5: 做 library aggregation

脚本多起来后：

- 聚类
- 合并
- 抽共享逻辑
- 做 review

### Phase 6: 需要时做 synthesis

如果工具库里没有合适工具，就进入 API/CLI synthesis：

- 给输入输出例子
- 生成新脚本
- 测试
- 修复

## 四、最推荐的实际目录

如果是一个要长期给 agent 用的 CLI 项目，我建议最少分成：

```text
tools/
  atomic/
  facades/
  libraries/
  indexes/
  evals/
```

职责：

- `atomic/`
  最小命令入口
- `facades/`
  高频任务脚本
- `libraries/`
  聚合后的共用工具层
- `indexes/`
  给 agent 检索的元信息
- `evals/`
  校验、回归、continuation scripts

## 五、真正该优化的不是“调用能力”，而是“检索质量”

这是最容易被忽略的点。

你现在有很多 CLI，不代表 agent 的工具能力强。

真正决定系统好坏的，通常是：

- 检索质量
- 选择质量
- 回退质量
- 验证质量

所以如果你现在要优化另一个项目，我建议优先顺序是：

1. 做工具索引
2. 做 task facade
3. 做 verification
4. 再做 maker-user
5. 最后做 library aggregation

## 一句话总结

这些论文在工程上的共同启发不是“让 agent 更会调命令”，而是：

**把工具系统从“命令集合”升级成“可检索、可规划、可复用、可治理的多层工具架构”。**
