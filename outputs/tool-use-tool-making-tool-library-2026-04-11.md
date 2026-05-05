# Tool Use、Tool Making、Tool Library 是一条连续演化线

日期：2026-04-11

## 结论

这三篇论文现在已经形成了一条完整分支：

1. `ToolLLM`
2. `LATM`
3. `ToolLibGen`

它们分别对应三个不同层次：

- 会用工具
- 会造工具
- 会组织工具库

## 为什么这不是三篇散论文

因为它们解决的是同一个系统不断上移的瓶颈：

### 1. ToolLLM

核心问题：

- 开源 LLM 为什么还不会稳定地使用大量真实 API

所以它补的是：

- 数据
- 检索
- 多步规划
- 评估

### 2. LATM

核心问题：

- 如果没有合适工具，为什么不让 LLM 先把工具造出来

所以它补的是：

- tool maker
- tool user
- functional cache
- 成本分工

### 3. ToolLibGen

核心问题：

- 当工具开始大量生成后，怎样避免工具库本身变成新的瓶颈

所以它补的是：

- tool clustering
- tool aggregation
- structured library
- retrieval scaling

## 这条线真正说明什么

它说明 agent/tool 系统成熟以后，瓶颈会不断上移：

- 先缺使用能力
- 再缺工具供给
- 再缺工具资产管理

所以一个系统越成熟，越不能只把问题理解成“模型会不会 function call”。

## 一句话判断

`ToolLLM -> LATM -> ToolLibGen` 这条线真正展示的是：  
LLM agent 的工具能力不是单点能力，而是一条从使用、生成到治理的系统演化线。
