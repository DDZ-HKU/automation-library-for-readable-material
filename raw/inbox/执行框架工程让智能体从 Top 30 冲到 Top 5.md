---
title: "执行框架工程让智能体从 Top 30 冲到 Top 5"
source: "https://skillnav.dev/articles/improving-deep-agents-with-harness-engineering"
author:
  - "[[SkillNav]]"
published: 2026-02-18
created: 2026-04-13
description: "文章介绍了 LangChain 如何通过执行框架工程显著提升其编码智能体 deepagents-cli 的性能。核心方法包括利用追踪分析技能自动化诊断错误、通过系统提示和中间件强制智能体进入“构建-验证”循环、为智能体注入环境上下文、以及采用“推理三明治”策略优化计算资源分配。这些实践为构建更强大的智能体应用提供了具体指导。"
tags:
  - "clippings"
---
深度LangChain2026年2月17日7 分钟阅读

![执行框架工程让智能体从 Top 30 冲到 Top 5](https://blog.langchain.com/content/images/size/w1200/2026/02/Screenshot-2026-02-12-at-12.25.20---PM.png)

LangChain 团队仅通过优化执行框架（Harness），就让其编码智能体在 Terminal Bench 2.0 上的得分从 52.8 提升至 66.5，排名从 Top 30 外跃升至 Top 5。他们分享了基于追踪分析和自验证等关键方法的执行框架工程实践。

我们的编码智能体在 [Terminal Bench 2.0](https://www.tbench.ai/leaderboard/terminal-bench/2.0?ref=blog.langchain.com) 上的排名从 Top 30 外冲到了 Top 5。我们只改了一样东西：执行框架（Harness）。这就是我们的执行框架工程方法（剧透：自验证和追踪分析帮了大忙）。

## 执行框架工程的目标

执行框架的目标，是把模型那种“时灵时不灵”的智能，塑造成能完成我们关心任务的形态。 **执行框架工程** 是关于系统的，你是在围绕模型构建工具，以优化任务性能、Token 效率、延迟等目标。设计决策包括系统提示、工具选择和执行流程。

但具体该怎么改执行框架，才能提升智能体呢？

在 LangChain，我们使用 [Traces](https://docs.langchain.com/langsmith/observability-quickstart?ref=blog.langchain.com) 来大规模理解智能体的失败模式。今天的模型很大程度上是黑盒，其内部机制难以解释。但我们可以看到它们在文本空间中的输入和输出，并以此作为改进循环的依据。

我们用一个简单的配方，迭代改进了 [deepagents-cli](https://github.com/langchain-ai/deepagents/tree/main/libs/cli?ref=blog.langchain.com) （我们的编码智能体），在 Terminal Bench 2.0 上的得分从 `52.8` 提升到了 `66.5` ，增加了 `13.7 分` 。我们只调整了执行框架，模型固定为 `gpt-5.2-codex` 。

![](https://blog.langchain.com/content/images/2026/02/Screenshot-2026-02-12-at-12.25.20---PM-1.png)

## 实验设置与执行框架的“旋钮”

我们使用了 [Terminal Bench 2.0](https://www.tbench.ai/?ref=blog.langchain.com) ，这是一个现在用于评估智能体编码能力的标准基准测试，包含 89 个跨机器学习、调试、生物学等领域的任务。我们用 [Harbor](https://harborframework.com/?ref=blog.langchain.com) 来编排运行。它会启动沙箱（ [Daytona](https://www.daytona.io/?ref=blog.langchain.com) ），与我们的智能体循环交互，并运行验证和评分。

每个智能体动作都存储在 [LangSmith](https://smith.langchain.com/?ref=blog.langchain.com) 中，还包括延迟、Token 计数和成本等指标。

### 我们可以调节的“旋钮”

一个智能体执行框架有很多旋钮：系统提示、工具、钩子/中间件、技能、子智能体委派、记忆系统等等。我们有意压缩了优化空间，聚焦于三个： **系统提示、工具** 和 **[中间件](https://docs.langchain.com/oss/python/langchain/middleware/overview?ref=blog.langchain.com#the-agent-loop)** （我们对模型和工具调用周围钩子的称呼）。

我们从默认提示和标准工具+中间件开始。这在使用 GPT-5.2-Codex 时得到了 52.8% 的分数。一个不错的分数，在当时的排行榜上刚好排在 Top 30 之外，但还有提升空间。

![](https://blog.langchain.com/content/images/2026/02/Screenshot-2026-02-16-at-12.50.00---PM.png)

### 追踪分析器技能

我们希望追踪分析是可重复的，所以把它做成了一个智能体技能。这构成了我们 **分析跨运行错误并改进执行框架** 的配方。流程如下：

1. 从 LangSmith 获取实验追踪数据。
2. 并行启动错误分析智能体 → 主智能体综合发现和建议。
3. 汇总反馈，并对执行框架进行有针对性的更改。

这类似于 [提升法](https://en.wikipedia.org/wiki/Boosting_\(machine_learning\)?ref=blog.langchain.com) ，专注于先前运行中的错误。人类在第 3 步中可能很有帮助（虽然不是必须的），用于验证和讨论提议的更改。过度拟合某个任务的更改不利于泛化，并可能导致其他任务出现性能回退。

自动化的追踪分析节省了大量时间，让我们能快速尝试实验。我们很快会发布这个技能，目前正在测试它用于一般的提示优化。

![](https://blog.langchain.com/content/images/2026/02/langsmith_trace_analyzer_skill.png)

## 真正提升智能体性能的因素

自动化追踪分析让我们能够 [调试智能体在哪里出错了](https://www.langchain.com/conceptual-guides/agent-observability-powers-agent-evaluation?ref=blog.langchain.com) 。问题包括推理错误、未遵循任务指令、缺少测试和验证、超时等。我们在下面的章节中更详细地介绍这些改进。

### 构建与自验证

今天的模型是卓越的自我改进机器。

**自验证允许智能体在一次运行中通过反馈进行自我改进** 。然而，它们并没有自然倾向进入这种 **构建-验证循环** 。

最常见的失败模式是：智能体写了一个解决方案，重读自己的代码，确认看起来没问题，然后就停止了。测试是自主智能体编码的关键部分。它有助于测试整体正确性，同时为智能体提供信号，使其能够朝着目标“爬坡”。

我们在系统提示中添加了关于如何解决问题的指导。

1. **规划与探索：** 阅读任务，扫描代码库，根据任务规范和如何验证解决方案制定初步计划。
2. **构建：** 带着验证的意识实施计划。构建测试（如果不存在），并测试正常路径和边界情况。
3. **验证：** 运行测试，读取完整输出，与任务要求（而不是与你自己的代码）进行比较。
4. **修复：** 分析任何错误，重新审视原始规范，并修复问题。

我们特别关注测试，因为它驱动着每次迭代的变化。我们发现，除了提示之外，确定性的上下文注入也有助于智能体验证其工作。我们使用一个 `PreCompletionChecklistMiddleware` ，它在智能体退出前进行拦截，提醒其根据任务规范运行验证流程。这类似于 [Ralph Wiggum 循环](https://ghuntley.com/loop/?ref=blog.langchain.com) ，一个钩子强制智能体在退出时继续执行，我们用它来进行验证。

![](https://blog.langchain.com/content/images/2026/02/self-verification-loop.png)

### 让智能体了解其环境

执行框架工程的一部分是 **为上下文工程构建良好的交付机制** 。Terminal Bench 任务附带目录结构、内置工具和严格的超时限制。

1. **目录上下文与工具：** 一个 `LocalContextMiddleware` 在智能体启动时运行，映射 `cwd` 和其他父/子目录。我们运行 `bash` 命令来查找像 `Python` 安装这样的工具。上下文发现和搜索容易出错，因此注入上下文可以减少这个错误面，并帮助 **智能体熟悉其环境** 。
2. **教智能体编写可测试的代码：** 智能体不知道它们的代码需要如何变得可测试。我们添加提示，说明它们的工作将根据程序化测试来衡量，类似于提交代码时的情况。例如，提到文件路径的任务规范应被严格遵守，以便解决方案能在自动化评分步骤中工作。强调边界情况的提示有助于智能体避免只检查“正常路径”情况。强制模型符合测试标准是避免随时间产生“马虎积累”的有力策略。
3. **时间预算：** 我们注入时间预算警告，以促使智能体完成工作并转向验证。智能体在时间估算方面臭名昭著地差，所以这种启发式方法在这种环境下很有帮助。现实世界的编码通常没有严格的时间限制，但如果不添加任何约束知识，智能体就不会在时间限制内工作。

智能体对其环境、约束和评估标准了解得越多，它们就越能自主地指导自己的工作。

**执行框架工程师的目的：准备并交付上下文，以便智能体能够自主完成工作。**

### 鼓励智能体退一步重新考虑计划

智能体一旦决定了计划，可能会变得短视，导致“死亡循环”，即对同一个错误方法进行微小变体（在某些追踪中超过 10 次）。

我们使用一个 `LoopDetectionMiddleware` ，它通过工具调用钩子跟踪每个文件的编辑次数。在对同一文件进行 `N` 次编辑后，它会添加上下文，如“……考虑重新评估你的方法”。这可以帮助智能体从死亡循环中恢复，尽管如果模型认为自己是正确的，它可能会继续沿着相同的路径走下去。

重要提示：这是一种设计启发式方法，旨在围绕当今感知到的模型问题进行工程化处理。随着模型的改进，这些安全护栏（Guardrails）很可能变得不必要，但今天有助于智能体正确且自主地执行。

### 选择在推理上花费多少计算资源

推理模型可以自主运行数小时，因此我们必须决定在每个子任务上花费多少计算资源。你可以在每个任务上都使用最大的推理预算，但大多数工作可以通过优化推理计算支出来受益。

Terminal Bench 的超时限制造成了权衡。更多的推理有助于智能体评估每个步骤，但可能会消耗超过 `2 倍` 的 Token/时间。 `gpt-5.2-codex` 有 4 种推理模式： `low` 、 `medium` 、 `high` 和 `xhigh` 。

我们发现，推理有助于规划以完全理解问题，一些 Terminal Bench 任务非常困难。一个好的计划有助于更快地找到可行的解决方案。

后期验证阶段也能从更多的推理中受益，以发现错误并提交解决方案。作为一种启发式方法，我们选择 xhigh-high-xhigh 的“ **推理三明治** ”作为基线。

![](https://blog.langchain.com/content/images/2026/02/the-reasoning-sandwich.png)

**在规划和验证上花费更多的推理计算资源**

仅在 `xhigh` 模式下运行由于智能体超时，得分较低，为 `53.9%` ，而 `high` 模式下为 `63.6%` 。在不同推理预算分配的试验运行中，差异不大，因此我们坚持了我们的方法，将分数推至 `66.5%` 。

模型的自然方法是 **自适应推理** ，这在 [Claude](https://platform.claude.com/docs/en/build-with-claude/adaptive-thinking?ref=blog.langchain.com) 和 [Gemini](https://ai.google.dev/gemini-api/docs/thinking?ref=blog.langchain.com) 模型中可以看到，模型自行决定在推理上花费多少计算资源。

在多模型执行框架中，平衡推理预算可能表现为使用大模型进行规划，然后 [移交](https://docs.langchain.com/oss/python/langchain/multi-agent/handoffs?ref=blog.langchain.com) 给小模型进行实施。

## 构建智能体执行框架的实用要点

智能体的设计空间很大。以下是我们实验和构建 deepagents 整体过程中得出的一些通用原则。

1. **代表智能体进行上下文工程。** 上下文组装对今天的智能体来说仍然很困难，尤其是在未见过的环境中。通过目录结构、可用工具、编码最佳实践和问题解决策略等上下文来引导模型，有助于减少因搜索不佳和规划中可避免错误而产生的错误面。
2. **帮助智能体自验证其工作。** 模型倾向于相信它们第一个看似合理的解决方案。积极提示它们通过运行测试和完善解决方案来验证工作。这在没有人工参与（Human-in-the-Loop）的自主编码系统中尤为重要。
3. **将追踪作为反馈信号。** 追踪允许智能体自我评估和调试。重要的是要一起调试工具和推理（例如：模型走错路是因为缺少工具或不知道如何做某事）。
4. **短期内检测并修复不良模式。** 今天的模型并不完美。执行框架设计师的工作是围绕当今的缺点进行设计，同时为未来更智能的模型做规划。盲目重试和不验证工作就是很好的例子。这些安全护栏几乎肯定会随着时间的推移而消失，但为了今天构建稳健的智能体应用，它们是值得试验的有用工具。
5. **为模型量身定制执行框架。** [Codex](https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide/?ref=blog.langchain.com) 和 [Claude](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices?ref=blog.langchain.com) 的提示指南表明，不同模型需要不同的提示方式。使用早期执行框架版本，Claude Opus 4.6 的测试运行得分为 `59.6%` ，有竞争力但比 Codex 差，因为我们没有对 Claude 运行相同的改进循环。许多原则是通用的，比如良好的上下文准备和对验证的关注，但为你的任务运行几轮执行框架迭代，有助于最大化智能体在不同任务上的性能。

在执行框架设计方面，还有更多开放的研究要做。有趣的途径包括多模型系统（Codex、Gemini 和 Claude 一起）、用于持续学习的记忆原语（以便智能体可以自主改进任务），以及跨模型衡量执行框架变化。

对于改进智能体的外层循环，我们正在研究像 [RLMs](https://alexzhang13.github.io/blog/2025/rlm/?ref=blog.langchain.com) 这样的方法，以更高效地挖掘追踪数据。我们将继续努力改进执行框架，并公开分享我们的研究。

我们创建了 [我们的追踪数据集](https://smith.langchain.com/public/29393299-8f31-48bb-a949-5a1f5968a744/d?tab=2&ref=blog.langchain.com) 与社区分享。

Deep Agents 是开源的。 [Python](https://github.com/langchain-ai/deepagents?ref=blog.langchain.com) 和 [Javascript](https://github.com/langchain-ai/deepagentsjs?ref=blog.langchain.com) 。

**为了更多的爬坡和开放研究。**

本文编译自 [Improving Deep Agents with harness engineering](https://blog.langchain.com/improving-deep-agents-with-harness-engineering/) ，版权归原作者所有。

觉得有用？分享给更多人