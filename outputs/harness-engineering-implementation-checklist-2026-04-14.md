# Harness 工程实施 Checklist

日期：2026-04-14

## 目标

把一个 agent 系统从“能跑”推进到“可控、可验证、可恢复、可扩展”。

## 一、启动前检查

开始设计 harness 前，先确认：

- 任务目标是否明确
- 是否知道主要失败模式是什么
- 是否知道哪些动作有副作用
- 是否知道是否需要长时运行
- 是否已经决定哪些规则要交给 LLM，哪些要交给 harness

如果这些都不清楚，不要急着加复杂组件。

## 二、Guide Layer Checklist

检查是否具备：

- 有一份短的总 guide，而不是巨型说明书
- 默认顺序清楚
- 关键边界清楚
- 规则是 agent-readable 的
- 规则没有和其它入口层文件重复堆叠

典型对象：

- `AGENTS.md`
- skills
- maps
- scoped instructions

验收标准：

- agent 知道先读什么
- agent 知道默认顺序
- 不需要反复人工解释同一类基本规则

## 三、Tool / Facade Layer Checklist

检查是否具备：

- atomic 工具仍保留
- 高频任务已抽成 facade
- facade 有明确输入格式
- facade 有明确输出格式
- facade 的失败格式可识别
- 副作用已标明

优先抽成 facade 的对象：

- 高频重复
- 顺序稳定
- 输出希望标准化
- agent 容易选错

验收标准：

- 高频任务不再靠手工拼原子命令
- agent 检索误用率下降
- 新人或低能力 agent 更容易选对入口

## 四、Sensor / Verification Layer Checklist

检查是否具备：

- deterministic checks 已优先建立
- 有 completion gate
- 有 readiness gate
- 有最小 review / verification loop
- 结果不是“看起来完成”，而是“可检查完成”

典型对象：

- tests
- linters
- review checks
- readiness scripts
- verification methods

验收标准：

- claim complete 前可验证
- handoff 前可验证
- 出错后能知道错在推理、环境、工具还是验证

## 五、State / Handoff Layer Checklist

检查是否具备：

- 关键状态已外置
- phase / task state 不只存在 prompt 里
- handoff artifact 结构固定
- restart point 明确
- verified / open risks 明确

最小 handoff 至少包括：

- 当前做到哪里
- 已验证什么
- 下一步是什么
- 风险是什么

验收标准：

- 中断后能恢复
- 新 session 不必重读全部历史
- stop / continue 的边界不会模糊

## 六、Protocol / Control Layer Checklist

检查是否具备：

- 默认执行循环已定义
- stop condition 已定义
- retry policy 已定义
- approval gate 已定义
- timeout / budget 策略已定义

典型对象：

- runbook
- workboard
- handoff rules
- retry cap

验收标准：

- agent 不会因为“感觉差不多”就停
- agent 不会无限重试
- agent 不会跨风险边界继续扩做

## 七、推荐落地顺序

最稳的顺序是：

1. 先做 guide
2. 再做少量稳定工具
3. 再抽 facade
4. 再补 deterministic verification
5. 再补 handoff artifact
6. 最后补 full protocol

不要一开始就上复杂多代理和重 orchestration。

## 八、验收标准

一套 harness 至少做到下面几点，才算从“能跑”进入“可控”：

- agent 知道默认入口
- 高频任务有 facade
- claim complete 前能验证
- 状态能外置
- 中断后能恢复
- stop condition 不是主观判断

## 九、常见故障排查

### 1. agent 过早收尾

优先检查：

- 有没有 completion gate
- 有没有 verification requirement
- 有没有 context anxiety

### 2. agent 反复走错工具

优先检查：

- tool 边界是否模糊
- 是否缺 facade
- 是否缺 curated tool subset

### 3. agent 死循环

优先检查：

- 是否缺 loop detection
- 是否缺真实反馈
- 是否让 agent 一直局部修补而不重审方案

### 4. handoff 后无法恢复

优先检查：

- handoff 是否只是日志而不是状态包
- 是否缺 verified / restart point
- 关键状态是否仍只存在上下文中

### 5. 系统越做越复杂却不更稳

优先检查：

- 是否把太多规则堆进 prompt
- 是否跳过 deterministic infrastructure
- 是否过早上多代理

## 十、一句话规则

如果你只能记住一条实施原则，就记住这一句：

**先把环境、反馈、状态和边界做稳，再扩大 agent 自主性。**

## 关联页面

- [harness-engineering-practice-report-and-component-rules-2026-04-14.md](/Users/ddz/Documents/exp/outputs/harness-engineering-practice-report-and-component-rules-2026-04-14.md)
- [agent-harness-engineering.md](/Users/ddz/Documents/exp/wiki/concepts/agent-harness-engineering.md)
- [how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md)
- [how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops.md)
- [how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md](/Users/ddz/Documents/exp/wiki/notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md)
