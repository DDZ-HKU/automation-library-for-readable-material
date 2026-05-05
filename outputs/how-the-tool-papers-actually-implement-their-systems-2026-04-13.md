# 这些 Tool 论文在工程上到底是怎么做的

日期：2026-04-13

## 这份说明在补什么

前面的产物已经把 `five patterns` 和 `how to apply` 讲清楚了，但如果要真正借鉴这些论文来设计系统，还需要再回答一层更工程化的问题：

- 每篇论文的系统到底怎么构建
- 它们用了哪些设计和技术
- 它们的“会用工具 / 会造工具 / 会组织工具库”不是一句口号，而是具体如何实现

这份说明就专门回答这些“实施细节”。

## 先给总图

把这几篇论文放在一起看，它们其实覆盖了四种不同实现问题：

1. `ToolLLM`
   问题：如何让模型在大量真实 API 上形成可训练、可评估的 tool-use 能力

2. `CREATOR`
   问题：如果工具不足，如何把抽象工具创建和具体决策执行分成不同阶段

3. `LATM`
   问题：如果工具可以被创建，如何把“造工具”和“用工具”的成本拆开

4. `ToolLibGen`
   问题：如果工具已经大量生成，如何把碎片工具重构成可检索的结构化库

5. `API Synthesis Using LLMs`
   问题：如果目标是直接合成新的 API 实现，而不是治理一组 agent 工具，系统该怎么做

所以它们不是同一个实现模板，而是五种不同的系统构造方式。

## 一、ToolLLM 是怎么做的

### 1. 它不是“给模型几个函数描述”那么简单

ToolLLM 真正搭的是一个完整训练与评估系统：

- `ToolBench`
- `ToolLLaMA`
- `API retriever`
- `DFSDT`
- `ToolEval`

也就是说，它不是只做 inference，而是把：

- 数据构造
- 模型训练
- 运行时检索
- 规划策略
- 自动评估

一起搭起来。

### 2. 数据怎么来的

它的数据构造分三步：

1. 收集真实 API
   - 从 RapidAPI 收集 16,464 个 REST APIs

2. 生成指令
   - 用 ChatGPT 生成涉及这些 API 的任务
   - 覆盖单工具和多工具场景

3. 标注解决路径
   - 不是只给答案，而是生成 chain of API calls

所以 ToolLLM 的关键不是“训练集很大”，而是：

- 它把 tool use 从单句问答变成了带执行路径的数据结构

### 3. 模型层怎么设计

它不是直接训练一个“万能 agent”，而是：

- 微调一个 LLaMA 变成 ToolLLaMA
- 额外加入 API retriever

这意味着运行时分工是：

- 检索器先缩小 API 空间
- 模型再在候选 API 上做推理和调用

### 4. 推理策略怎么设计

它没有停在普通 ReAct。

引入了：

- `DFSDT`（depth-first search-based decision tree）

其本质是：

- 展开多条 reasoning trace
- 允许回退
- 选择更有前景的路径

也就是说，它已经不再假设“一次 linear reasoning 就够”。

### 5. 评估怎么做

它引入了 `ToolEval`，至少有两个核心指标：

- pass rate
- win rate

这很重要，因为 tool-use 问题不是单一正确答案，而常常是多条路径都可能正确。

所以 ToolLLM 的真正工程启发是：

- **tool use 必须把数据、检索、规划和评估一起设计**

## 二、CREATOR 是怎么做的

### 1. 它的关键不是“会造工具”，而是“怎么拆阶段”

CREATOR 真正的系统创新是把整个过程拆成四段：

1. `Creation`
2. `Decision`
3. `Execution`
4. `Rectification`

这和一般 tool-use 框架的最大不同是：

- 不再把“创造工具”和“决定怎么用工具”压在同一步

### 2. 它为什么要这么拆

论文明确认为，当前 tool-augmented LLM 的问题不只是：

- 工具不够多

还包括：

- 推理脆弱
- scope 不够
- 缺乏错误修正

所以它的设计判断是：

- 抽象工具创建需要一种 reasoning
- 具体求解中的 decision 又是另一种 reasoning

如果混在一起，LLM 负担会太重。

### 3. 技术上怎么体现

CREATOR 让模型先：

- 通过抽象 reasoning 设计一般工具

再：

- 在具体问题上决定何时、如何使用这些工具

然后：

- 执行
- 根据执行错误做 rectification

这使它比普通 tool use 多出一整层“自修正工具链”。

### 4. 它用了哪些技术

从当前材料可确认，它主要依赖：

- CoT / PoT 风格推理背景
- code 作为工具媒介
- error-driven rectification
- hints 来提高工具创建成功率

重点不在外部 retriever，而在：

- **把推理结构拆开**

### 5. 它的工程启发

CREATOR 最值得借鉴的不是具体 benchmark，而是：

- **当系统既要“造工具”又要“用工具”时，必须分阶段，而不能让一个 prompt 同时做所有事。**

## 三、LATM 是怎么做的

### 1. 它和 CREATOR 的区别

CREATOR 重点是认知分工。

LATM 重点是成本分工。

LATM 把系统拆成：

- tool maker
- tool user

### 2. 它真正想解决的问题

不是“如何让每次问题都更聪明地解”，而是：

- 在多次请求场景下
- 如何把高能力模型的成本摊掉

### 3. 具体怎么搭

它的系统结构是：

- 高能力模型，比如 GPT-4，负责生成 reusable Python tools
- 低成本模型，比如 GPT-3.5，负责后续使用这些 tools 解类似任务

所以运行链条是：

1. 遇到任务类
2. 高能力模型造工具
3. 工具缓存下来
4. 后续请求由低成本模型调用

### 4. 它的关键技术点

- Python utility functions 作为工具载体
- maker/user 分层
- functional cache

这里的 functional cache 很关键：

- 缓存的不是自然语言回答
- 缓存的是“解决这类问题的功能”

### 5. 它的工程启发

LATM 最值得借鉴的是：

- **把“造工具”看成高成本前置投资，把“用工具”看成低成本批量执行。**

这对你设计 CLI 系统非常有用，因为：

- 高能力 agent 可以先把原子命令封装成项目脚本
- 低成本 agent 再大量使用这些脚本

## 四、ToolLibGen 是怎么做的

### 1. 它解决的是规模化后的第二问题

Tool making 一旦成功，系统会进入新的痛点：

- 工具太多
- 检索太难
- 功能太重叠

ToolLibGen 的系统就是围绕这个问题搭的。

### 2. 它的流程分成哪几步

从当前材料可确认，它至少分四步：

1. question-specific tool creation
2. tool clustering
3. tool aggregation
4. tool-augmented reasoning

### 3. 它的关键设计

最重要的不是“自动聚类”本身，而是：

- 先按功能聚类
- 再把一个 cluster 内的离散工具聚合成更少但更一般的工具

也就是说，它解决的是：

- 不只是减少工具数量
- 而是减少检索歧义

### 4. 多 agent 怎么参与

论文明确用了一个 multi-agent framework：

- code agent
- reviewing agent

代码 agent 负责：

- 重构代码
- 抽共享逻辑
- 生成 aggregated tools

reviewing agent 负责：

- 检查功能是否丢失
- 确认聚合后仍覆盖原来工具的能力

### 5. 它的工程启发

ToolLibGen 最值得借鉴的是：

- **工具多了以后，不能继续平铺；必须进入聚类、聚合、治理。**

这对 CLI 系统的直接启发是：

- 脚本开始多起来后，不能只靠命名和文件夹顶着
- 应当开始做功能聚类和共享逻辑抽取

## 五、API Synthesis Using LLMs 是怎么做的

### 1. 它和前面几篇不在同一主线上

前面几篇主要是：

- tool use
- tool making
- tool library

而这篇是：

- API synthesis / program synthesis

### 2. 它解决的问题

不是“让模型管理已有工具”，而是：

- 给输入输出示例和 API 签名
- 让模型直接综合出可执行 API 实现

### 3. 它怎么做

当前材料显示，它主要依赖：

- assistant creation
- chain of thought
- few-shot learning
- follow-up prompts

然后用：

- compile
- test pass
- readability

这些维度去评估。

### 4. 它的比较对象

它对比的是：

- FrAngel
- 其他 component-based API synthesis 方法

所以它本质上是在说：

- LLM 可以替代一部分传统显式搜索与 formal specification 负担

### 5. 它的工程启发

这篇最值得借鉴的是：

- **当问题本质是“综合一个新实现”时，不必硬套到 tool governance 主线里。**

你应该承认它是一条旁支：

- synthesis
- 而不是 reuse/governance

## 六、把五篇放在一起，应该怎么学

最稳的学习顺序不是按年份，而是按系统层：

### 第 1 层：会用

看 ToolLLM

关注：

- 数据怎么造
- 检索怎么接
- 规划怎么做
- 评估怎么定义

### 第 2 层：会造

看 CREATOR 和 LATM

关注：

- creation 如何分阶段
- maker/user 如何分工
- rectification 或 cache 如何介入

### 第 3 层：会管

看 ToolLibGen

关注：

- clustering
- aggregation
- retrieval scaling
- multi-agent review

### 第 4 层：旁支综合

看 API Synthesis Using LLMs

关注：

- 什么时候该直接合成实现
- 什么时候该走 tool creation / tool library 路线

## 七、一句话总结

这些论文在工程上的真正贡献，不只是提出新词，而是分别把系统搭在了不同位置上：

- ToolLLM：搭数据、检索、规划、评估
- CREATOR：搭 creation / decision / execution / rectification 分层
- LATM：搭 maker-user serving 分工和 functional cache
- ToolLibGen：搭 tool clustering / aggregation / review 闭环
- API Synthesis：搭输入输出示例驱动的实现综合流程

所以你如果要借鉴它们，不该只抄“概念名”，而应该看清它们各自把系统边界放在哪一层。  
