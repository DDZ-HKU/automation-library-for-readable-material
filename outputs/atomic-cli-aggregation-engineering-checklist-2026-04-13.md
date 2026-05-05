# CLI 原子化聚合：工程落地 Checklist 版

日期：2026-04-13

## 目标

把已经原子化的 CLI，逐步提升成可复用、可检索、可治理的工具体系。

## 一、先判断哪些命令该聚合

满足以下任意两个条件，就进入候选列表：

- 高频重复
- 顺序稳定
- 输出希望标准化
- agent 经常选错
- 多个命令总是一起出现

不满足的，先继续保持原子。

## 二、不要聚合这些对象

先不要动这几类：

- 低频命令
- 探索性强的调试命令
- 组合方式高度不确定的命令
- 只在特殊场景下用一次的命令

## 三、第一批只做 5 到 10 个 facade

优先抽下面这类：

- 搜索类
- 状态检查类
- 验证类
- 预处理类
- 高频固定流程类

不要一上来做几十个。

## 四、每个 facade 必须补齐的字段

每个 facade 至少明确：

- 名称
- 目的
- 输入格式
- 输出格式
- 失败格式
- 是否有副作用

如果这些写不清，不要暴露给 agent。

## 五、推荐的聚合实现方式

### 方式 1：Pipeline Wrapper

适用：

- 固定顺序
- 少分支
- 易验证

### 方式 2：Task Facade

适用：

- 高频任务
- 任务语义明确
- 需要稳定输入输出

### 方式 3：Maker-User Split

适用：

- 高能力 agent 或资深工程师负责抽象
- 普通 agent 负责稳定调用

### 方式 4：Library Aggregation

适用：

- 脚本已经明显增多
- 检索歧义开始出现
- 需要按功能合并和抽共享逻辑

## 六、实现时的最小检查表

### Atomic Layer

- 保留底层原语
- 不删除探索性命令
- 标清只读 / 可写 / 高风险

### Facade Layer

- facade 名称反映任务，而不是反映内部命令
- 输入输出格式稳定
- 失败格式可识别
- 副作用明确

### Planning Layer

- 明确先调哪个 facade
- 明确失败后回退方式
- 明确何时验证
- 明确何时停止

### Governance Layer

- 同类工具开始分类
- 重叠功能开始聚合
- 检索入口单独建立
- 命名风格统一

## 七、什么时候要停止继续加 facade

出现这些信号时，不要继续机械加 facade，而该转向治理：

- 同类 facade 超过数个
- 功能开始重叠
- 名字相似但边界不同
- agent 开始选错
- 你需要专门解释每个 facade 差别

## 八、验收标准

一批聚合工作完成后，至少确认：

- 高频任务不再依赖手工拼原子命令
- agent 误用率下降
- 输出格式比之前稳定
- 新人或低能力 agent 更容易选对工具
- 工具数量增加后仍能找到正确入口

## 九、最容易漏掉的点

- 只包脚本，不定义失败格式
- facade 名字仍然太底层
- 聚合后没有建立检索入口
- 工具变多了还没有分类
- 继续把高频组合留给普通 agent 手工拼接

## 十、最短执行顺序

1. 盘点高频原子命令组合
2. 挑出前 5 到 10 个候选
3. 为每个候选定义输入/输出/失败边界
4. 实现 facade
5. 让 agent 先走 facade，不再默认走原子层
6. 当 facade 开始增多，再做分类、聚类和统一接口

## 关联页面

- [how-to-aggregate-atomic-cli-after-atomization-2026-04-13.md](/Users/ddz/Documents/exp/outputs/how-to-aggregate-atomic-cli-after-atomization-2026-04-13.md)
- [how-to-aggregate-atomic-cli-commands-for-agents.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-aggregate-atomic-cli-commands-for-agents.md)

