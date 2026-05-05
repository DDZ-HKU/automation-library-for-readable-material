# CLI 原子化之后如何聚合

日期：2026-04-13

## 这份文档回答什么

如果你已经把 CLI 做成了很多原子命令，接下来的关键问题不再是：

- 命令能不能调用

而是：

- 哪些命令应该继续保持原子
- 哪些命令应该被包装成更高层入口
- 什么时候该从“会用命令”升级到“会管理工具体系”

一句话结论：

**原子化是起点，不是终点。最稳的路线是：原子命令保底，任务门面做主力，maker-user 分层做演化，工具库聚合做规模化。**

## 一、先明确“聚合”不是把文件放一起

CLI 原子化之后的“聚合”，不是简单地：

- 把几个命令写进一个脚本
- 或把很多脚本塞进同一个目录

真正的聚合是在解决 4 个更高层问题：

1. 降低检索负担
2. 降低误用率
3. 稳定输入输出
4. 让高频任务不必每次从零规划

所以聚合的对象不是“文件数”，而是：

- 重复动作链
- 稳定任务单元
- 可复用工具资产

## 二、原子化之后的 4 层结构

### 1. Atomic Layer

保留底层原语。

典型例子：

- `rg`
- `ls`
- `sed`
- `git status`
- `pytest`
- `curl`

这一层适合：

- 探索
- 调试
- 临时试探
- 未知路径下的小步动作

但它不适合长期承担主工作流，因为：

- agent 每次都要自己检索
- 每次都要自己拼顺序
- 每次都要自己适配输出

### 2. Facade Layer

把高频、顺序稳定、语义明确的动作链包装成任务入口。

典型例子：

- `scripts/kb search`
- `scripts/pdf-to-md`
- `scripts/ops-phase-status`

这一层的价值不是省几条命令，而是：

- 把动作变成“任务”
- 把选择空间变小
- 把输入输出变稳定

### 3. Planning Layer

当原子命令和 facade 都存在时，还需要一个上层来决定：

- 先用哪个
- 失败后怎么回退
- 何时验证
- 何时停止

这一层不一定是脚本，也可以是：

- planner
- skill route
- search-based planning
- runbook

### 4. Library / Governance Layer

当 facade 和项目脚本越来越多后，新的问题变成：

- 名字开始重叠
- 功能开始重复
- agent 检索开始选错
- 维护成本开始上升

这时就必须进入工具库治理：

- 分类
- 聚类
- 抽共享逻辑
- 统一接口
- 建立检索入口

## 三、哪些原子 CLI 该聚合

一组原子 CLI 满足以下任意两个条件，就值得优先聚合：

1. 高频重复
2. 顺序稳定
3. 输出需要标准化
4. agent 经常在这里选错
5. 多个命令总是一起出现

例如：

- 搜索知识页
- 查 phase 状态
- 检查 handoff readiness
- PDF 预处理

这些都不是一次性临时动作，而是稳定任务单元。

## 四、哪些原子 CLI 不该急着聚合

有些命令最好继续保持原子：

- 探索性很强
- 使用频率低
- 组合方式高度不确定
- 更像调试原语而不是任务入口

例如：

- 单次 `rg`
- 单次 `sed`
- 临时 `git diff`
- 很具体的测试命令

原则是：

**原子层负责保底灵活性，facade 层负责主流程稳定性。**

## 五、最实用的聚合方法

### 方法 1：Pipeline Wrapper

把固定顺序的原子命令包装成一个脚本。

适合：

- 步骤固定
- 输出链稳定
- 失败点少

例如：

- `pdf -> markdown -> target path`

### 方法 2：Task Facade

给高频任务一个更高语义的入口。

适合：

- 任务名字比命令名字更重要
- agent 需要“知道什么时候用”

例如：

- `kb search`
- `ops-check-handoff-readiness`

### 方法 3：Maker-User Split

让高能力 agent 负责观察和造工具，让普通 agent 负责用工具。

适合：

- 已经存在明显重复组合
- 普通 agent 还在手工拼命令

它的价值在于：

- 一次抽象，多次复用
- 把高成本判断前置

### 方法 4：Library Aggregation

当工具越来越多后，把同类脚本聚类、合并、抽共享逻辑。

适合：

- 已经不缺脚本，反而脚本太多
- 检索歧义开始明显
- 同类工具名字相似但功能不同

## 六、推荐的落地顺序

最稳的推进顺序是：

1. 保留原子 CLI，不要删
2. 先抽 5 到 10 个最高频 facade
3. 给 facade 明确输入边界、输出边界、失败格式
4. 让高能力 agent 开始观察和生成项目专用脚本
5. 当 facade 和脚本开始变多，再做库化聚合

不要一上来就做“大一统工具平台”，那通常会过早抽象。

## 七、聚合后的设计要求

一个合格的聚合结果，至少要满足：

- 输入边界清楚
- 输出格式稳定
- 失败情况可识别
- 副作用明确
- 命名能反映任务语义

如果这些做不到，说明它还不适合作为 facade 暴露给 agent。

## 八、什么时候说明你已经该进入工具治理阶段

出现下面任一现象，就说明不能再只靠“多加脚本”了：

- 名字像但功能不同
- 功能重叠但名字不同
- agent 检索经常选错
- 同类脚本持续增加
- 你开始靠口头记忆哪个脚本该怎么用

这时重点应转向：

- metadata
- 分类
- 检索入口
- 统一接口

## 九、最容易犯的错误

- 以为原子化完成就结束了
- 过早把低频命令也包装成 facade
- 只包脚本，不稳定输入输出
- 工具已经很多了，还不做分类和治理
- 让普通 agent 持续手工拼高频命令组合

## 十、一句话操作建议

如果你现在已经有一批原子化 CLI，下一步不要继续“再多做几个原子命令”，而是：

**先找出最常重复、顺序最稳定、最容易误用的 5 到 10 组命令，把它们提升成 facade；等 facade 变多后，再进入工具库治理。**

## 关联页面

- [how-to-aggregate-atomic-cli-commands-for-agents.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-aggregate-atomic-cli-commands-for-agents.md)
- [how-agents-should-plan-and-improve-atomic-cli-usage.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-agents-should-plan-and-improve-atomic-cli-usage.md)
- [how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md)
- [five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md](/Users/ddz/Documents/exp/outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md)
