# Five Patterns 与 How To Apply 详细讲解

日期：2026-04-13

## 这份指南在回答什么

你现在已经有很多原子化 CLI/API 可以交给 agent 调用。真正困难的地方已经不再是：

- agent 能不能调用命令

而是：

- agent 应该怎么规划这些命令的使用
- 这些命令应该如何从“原子操作”演化成“可复用工具体系”
- 什么时候该保持原子，什么时候该包装，什么时候该库化

这份指南对应的核心框架页是：

- [how-agents-should-plan-and-improve-atomic-cli-usage.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-agents-should-plan-and-improve-atomic-cli-usage.md)

但这里会展开到人类可以直接拿去设计系统的粒度。

## 先给一句总判断

如果把原子化 CLI 全部直接暴露给 agent，短期会很灵活，长期会很乱。

最稳的路线是：

1. 保留原子命令作为底层动作
2. 把高频组合提升成任务门面
3. 让高能力 agent 开始造项目工具
4. 当工具变多后做库化聚合

也就是：

**原子命令保底，任务门面做主力，maker-user 分层做演化，工具库聚合做规模化。**

## 一、先理解 agent 在原子 CLI 面前到底在做什么

一个 agent 真正面对很多原子 CLI 时，并不是在“使用命令行”，而是在做一个小型决策系统：

1. 检索有哪些动作可用
2. 判断当前问题属于哪类任务
3. 选择一个或多个原子动作
4. 看执行后的环境反馈
5. 决定继续、回退、验证、还是停止

所以原子 CLI 本质上是 agent 的 **外部动作原语**。

这和你刚整理的 ToolLLM / CREATOR / LATM / ToolLibGen 主线是一致的：

- ToolLLM 告诉我们：真正的 tool use 不是单次 function call，而是一整条检索、规划、执行、评估链
- CREATOR 告诉我们：有些能力需要把“抽象创建”和“具体决策”拆开
- LATM 告诉我们：更高能力 agent 可以负责造工具，低成本 agent 负责使用工具
- ToolLibGen 告诉我们：工具多了以后，核心瓶颈会上移到组织与检索

所以你面对的已经不是“命令行技巧问题”，而是一个完整的 agent tool system 问题。

## 二、Five Patterns 详细展开

### Pattern 1: Atomic Call

这是最底层的模式。

典型形态：

- `rg`
- `ls`
- `sed`
- `git status`
- `pytest some/test.py`
- `curl ...`

### 它什么时候有价值

- 任务非常临时
- 需要探索而不是固定流程
- 需要细粒度调试
- 命令组合高度不确定

### 它的优点

- 灵活性最高
- 组合空间最大
- agent 能在未知场景里快速试探

### 它的缺点

- 检索负担高
- 误用率高
- 结果输出不稳定
- 难以规模化复用

### 最重要的判断

Atomic call 适合作为 **原语层**，不适合作为 **主工作流层**。

如果一个团队长期还靠 agent 直接手工组合很多原子 CLI 才能完成高频任务，通常说明：

- 还没有升到任务门面层

---

### Pattern 2: Task Facade

这是最重要的一层，也是最值得优先建设的一层。

典型形态：

- `scripts/kb search`
- `scripts/pdf-to-md`
- `scripts/ops-phase-status`
- `scripts/ops-check-handoff-readiness`

### 它在做什么

把多个原子命令包装成一个 **高语义、低歧义** 的任务入口。

对 agent 来说，这一层最重要的价值不是省几条命令，而是：

- 降低选择空间
- 稳定输入输出
- 把“什么时候用”变得更容易学

### 为什么这是主力层

原子 CLI 的问题不在底层能力，而在于：

- agent 每次都要重新检索
- 每次都要重新决定顺序
- 每次都要重新适配输出格式

Task facade 直接把这些不必要的重复判断去掉。

### 什么东西应该被提升成 facade

满足以下任意两个条件，就很适合升格：

1. 高频重复
2. 顺序稳定
3. 输出希望标准化
4. agent 经常在这里选错命令
5. 多个原子命令总是一起出现

### 这个模式在论文里的对应

- ToolLLM 的 API retriever + evaluator 其实就是在降低“agent 从大工具空间里检索”的成本
- 你当前仓库里的 `scripts/kb` 也是同类思想：不是让 agent 每次都自己用 `rg` 去扫整个 `wiki/`

---

### Pattern 3: Search-Based Planning

这类模式对应 ToolLLM / DFSDT 这种更复杂的工具使用。

### 它解决的问题

当：

- 原子动作很多
- 候选路径不止一条
- 多条路径都可能正确
- 错误路径需要回退

单次 ReAct 式线性规划就不够了。

### 它的核心

不是“一次想好所有步骤”，而是：

- 比较多条候选路径
- 允许回退
- 用环境反馈重选

### 什么时候该用

- 工具空间很大
- 多步骤规划复杂
- 正确路径不唯一
- 单路径推理误差代价高

### 它和 Atomic / Facade 的关系

Search-based planning 不是工具本身，而是工具之上的 **规划策略层**。

也就是说：

- Atomic / Facade 是动作层
- Search-based planning 是动作选择层

### 风险

如果没有好的 evaluator 和回退条件，它会：

- 搜太多
- 想太多
- 调太多无关工具

所以它必须和：

- verification
- stop condition
- trace

绑在一起。

---

### Pattern 4: Maker-User Split

这是 LATM 最关键的启发。

### 它的核心思想

不要默认：

- 同一个 agent
- 既负责造工具
- 又负责长期大量使用工具

更稳的做法是：

- 高能力 agent 负责造工具
- 低成本 agent 负责用工具

### 在 CLI 世界里的含义

这意味着：

- 高能力 agent 观察高频命令组合
- 把它们抽成脚本/中层工具
- 之后日常 agent 直接用这些脚本

### 它为什么重要

因为如果你不做 maker-user split，普通 agent 会一直陷在：

- 手工拼原子命令
- 重复造轮子
- 每次都从零规划

### 它在长期系统里的作用

maker-user split 是从“短期会用工具”走向“长期会长出工具资产”的关键一步。

没有这一步，就很难真正进入 ToolLibGen 说的工具库治理阶段。

---

### Pattern 5: Library Aggregation

这是规模化之后的关键模式，也是大多数系统最后都会面对的问题。

### 它解决的问题

当 task facade 和 maker-user 路线成功以后，新的问题一定会出现：

- 工具越来越多
- 命名越来越乱
- 功能开始重叠
- agent 不知道用哪个

这就是 ToolLibGen 的问题。

### 它的核心动作

1. 聚类
2. 提炼共享逻辑
3. 合并重叠工具
4. 重构统一接口
5. 建立结构化目录和检索入口

### 它不是在做什么

它不是简单地：

- 删重复文件
- 把几个函数扔一个目录

它做的是更高层的：

- 工具资产治理

### 对当前工程最重要的提醒

如果你已经开始有很多脚本，却还没有：

- 分类
- 元数据
- 清晰命名
- 检索入口

那系统其实已经进入 ToolLibGen 的问题域了，只是你还没承认。

## 三、How To Apply 详细展开

### Step 1: 把原子 CLI 做成“受控底层”

不要一上来删掉原子 CLI。

你需要保留：

- 搜索原语
- 文件原语
- git 原语
- 测试原语
- 网络原语

但要给它们标清：

- 只读 / 可写 / 高风险
- 输出是否稳定
- 是否允许直接暴露给一般 agent

### Step 2: 先做 5 到 10 个高频任务门面

不要试图一口气库化全部 CLI。

最正确的先手是：

- 从最常重复的工作流中抽 5 到 10 个 facade

例如：

- 搜知识
- 转 PDF
- 查 phase 状态
- 查 handoff readiness
- 做 continuation verification

### Step 3: 给每个 facade 建“输入边界”和“输出边界”

一个好 facade 至少要明确：

- 输入格式
- 输出格式
- 失败格式
- 是否有副作用

这样 agent 才能学会：

- 什么时候该调用
- 调完后怎么接下一步

### Step 4: 让高能力 agent 开始“造项目脚本”

也就是 maker-user split：

- 观察哪些原子命令组合总在重复
- 把它们升成 facade
- 再交给普通 agent 日常调用

### Step 5: 工具开始多起来后，马上做分层目录

建议至少分成：

- `atomic`
- `facades`
- `ops`
- `retrieval`
- `verification`
- `build`

### Step 6: 当 facade 超过阈值时，进入 library aggregation

阈值不必很高。

一旦出现以下现象，就该开始：

- 名字像但功能不同
- 功能重叠但名字不同
- agent 检索经常选错
- 同类脚本数量持续增长

### Step 7: 把能力提升目标从“多调命令”改成“少走错路”

这是最容易被忽略的点。

agent 工具能力提升，真正该优化的不是：

- 一次能调多少命令

而是：

- 检索错率
- 排序错率
- 回退能力
- 验证意识
- 停止判断

## 四、一个可直接照着用的架构

你可以直接把当前项目的工具体系按下面方式理解：

### A. Atomic Layer

- `rg`
- `sed`
- `git status`
- `pytest`

### B. Facade Layer

- `scripts/kb`
- `scripts/pdf-to-md`
- `scripts/ops-phase-status`
- `scripts/ops-check-handoff-readiness`
- `scripts/ops-verify-continuation`

### C. Planning Layer

- `kb-autonomous-run`
- `ops/runbook.md`

### D. Governance Layer

- `ops/workboard.md`
- `ops/handoff.md`
- continuation scripts

这就是从论文理解落到你当前工程上的最小版本。

## 五、一句话总结

这五种模式不是互斥选项，而是一条逐级上升的路线：

**Atomic Call -> Task Facade -> Search-Based Planning -> Maker-User Split -> Library Aggregation**

你真正该做的，不是问“哪一种最先进”，而是判断：

- 你现在的系统卡在哪一层
- 然后往上一层推进

## 论文支撑

这份讲解主要建立在当前知识库已入库的 tool 主线材料上：

- [ToolLLM](/Users/ddz/Documents/exp/wiki/sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md)
- [LATM](/Users/ddz/Documents/exp/wiki/sources/large-language-models-as-tool-makers.md)
- [CREATOR](/Users/ddz/Documents/exp/wiki/sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md)
- [ToolLibGen](/Users/ddz/Documents/exp/wiki/sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md)
- [API Synthesis Using LLMs](/Users/ddz/Documents/exp/wiki/sources/an-approach-for-api-synthesis-using-large-language-models.md)
