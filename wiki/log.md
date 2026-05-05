# Log

## [2026-04-07] refactor | initialize-llm-wiki-scaffold

创建 LLM Wiki 初始仓库骨架，包括：

- `raw/` 原始资料层
- `wiki/` 知识层
- `templates/` 页面模板
- `AGENTS.md` 代理工作协议
- 初始 `index.md`、`overview.md`、`log.md`

## [2026-04-07] refactor | simplify-to-raw-wiki-outputs

将仓库调整为更扁平的三层工作流：

- `raw/` 用于堆放原始资料
- `wiki/` 由 LLM 持续维护
- `outputs/` 用于保存答案、简报和报告
- 索引入口统一为 `wiki/INDEX.md`

## [2026-04-08] ingest | The First Law of Complexodynamics

处理 `raw/The First Law of Complexodynamics.md`，完成首份真实资料入库：

- 新建资料摘要页 `wiki/sources/the-first-law-of-complexodynamics.md`
- 新建概念页 `wiki/concepts/complextropy.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-08] ingest | The Unreasonable Effectiveness of Recurrent Neural Networks

处理 `raw/The Unreasonable Effectiveness of Recurrent Neural Networks.md`：

- 新建资料摘要页 `wiki/sources/the-unreasonable-effectiveness-of-recurrent-neural-networks.md`
- 新建概念页 `wiki/concepts/recurrent-neural-networks.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-08] ingest | Understanding LSTM Networks

处理 `raw/Understanding LSTM Networks -- colah's blog.md`：

- 新建资料摘要页 `wiki/sources/understanding-lstm-networks.md`
- 更新概念页 `wiki/concepts/recurrent-neural-networks.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-08] ingest | Recurrent Neural Network Regularization

处理 `raw/Obsidian.pdf.md`，识别其实际内容为 Zaremba 等关于 LSTM dropout 的论文文本：

- 新建资料摘要页 `wiki/sources/recurrent-neural-network-regularization.md`
- 更新概念页 `wiki/concepts/recurrent-neural-networks.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-08] query | rnn-lstm-phase-summary

基于当前 3 份 RNN/LSTM 资料生成阶段总结并保存到 `outputs/rnn-lstm-phase-summary-2026-04-08.md`：

- 汇总现象层、机制层与训练层认识
- 明确当前已建立的判断与仍待补的空白
- 更新 `wiki/INDEX.md`

## [2026-04-08] query | rnn-next-research-directions

基于当前 RNN/LSTM 主题线生成下一阶段研究提纲并保存到 `outputs/rnn-next-research-directions-2026-04-08.md`：

- 明确下一阶段应转向 Transformer / attention 对照视角
- 列出关键问题与资料补充顺序
- 更新 `wiki/INDEX.md`

## [2026-04-09] ingest | Order Matters: Sequence to Sequence for Sets

处理 `raw/sources/1511.06391v4/1511.06391v4.md`，识别其内容为 Vinyals 等关于 seq2seq 在集合输入/输出上扩展的论文：

- 新建资料摘要页 `wiki/sources/order-matters-sequence-to-sequence-for-sets.md`
- 新建概念页 `wiki/concepts/sequence-to-sequence-for-sets.md`
- 更新概念页 `wiki/concepts/recurrent-neural-networks.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] ingest | The Annotated Transformer

处理 `raw/The Annotated Transformer.md`，将其作为 Transformer 原始论文的注释版实现材料入库：

- 新建资料摘要页 `wiki/sources/the-annotated-transformer.md`
- 新建概念页 `wiki/concepts/transformers.md`
- 更新概念页 `wiki/concepts/sequence-to-sequence-for-sets.md`
- 更新概念页 `wiki/concepts/recurrent-neural-networks.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] query | pdf-to-markdown-preprocessing

将本地 `marker` 驱动的 PDF 预处理流程沉淀进知识库：

- 新建笔记页 `wiki/notes/pdf-to-markdown-preprocessing.md`
- 记录 `raw/inbox -> scripts/pdf-to-md -> raw/sources` 工作流
- 记录已验证样例 `1511.06391v4.pdf`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] ingest | GPipe: Easy Scaling with Micro-Batch Pipeline Parallelism

处理 `raw/sources/1811.06965v5/1811.06965v5.md`，识别其内容为 GPipe 关于超大模型流水线并行训练的论文：

- 新建资料摘要页 `wiki/sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md`
- 新建概念页 `wiki/concepts/pipeline-parallelism.md`
- 更新概念页 `wiki/concepts/transformers.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] refactor | add-tacit-knowledge-layer

将“默会知识解读”正式加入知识库设计：

- 更新 `AGENTS.md`，把 `wiki/notes/` 明确为默会知识层
- 更新 `README.md`，区分 sources / concepts / notes / outputs 的职责
- 新建说明页 `wiki/notes/tacit-knowledge-layer.md`
- 新建首篇默会知识页 `wiki/notes/tacit-knowledge-on-rnn-to-transformer-transition.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] query | architecture-optimization-systems-template

新增一篇更通用的默会知识判断模板：

- 新建笔记页 `wiki/notes/how-to-distinguish-architecture-optimization-and-systems-problems.md`
- 将“架构问题 / 优化问题 / 系统问题”的区分方法沉淀为可复用框架
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] query | model-paper-reading-template

新增一篇面向论文阅读的默会知识模板：

- 新建笔记页 `wiki/notes/how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value.md`
- 将“机制 / 瓶颈 / 迁移价值”的阅读方法沉淀为可复用框架
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] refactor | organize-notes-into-workflows-frameworks-cases

优化 `wiki/notes/` 的结构，使默会知识层更清晰：

- 将操作流程归入 `wiki/notes/workflows/`
- 将通用判断模板归入 `wiki/notes/frameworks/`
- 将主题型默会知识页归入 `wiki/notes/cases/`
- 更新 `AGENTS.md`
- 更新 `README.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] query | research-reading-and-decision-stack

新增一页总导航框架，把默会知识层中的阅读与判断模板串成完整流程：

- 新建笔记页 `wiki/notes/frameworks/research-reading-and-decision-stack.md`
- 将问题分层、机制/瓶颈阅读、案例解释与知识库动作接成一条链
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] query | paper-reading-to-research-decisions

新增一页决策模板，把论文阅读进一步推进到研究动作：

- 新建笔记页 `wiki/notes/frameworks/how-to-turn-paper-reading-into-research-decisions.md`
- 将阅读结果映射为继续、对照、提炼或降级等研究动作
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-09] query | rnn-transformer-research-decision-memo

基于当前 `RNN/LSTM -> Transformer -> GPipe` 主题线生成一份下一阶段研究决策 memo 并保存到 `outputs/rnn-transformer-research-decision-memo-2026-04-09.md`：

- 明确当前最稳的三条判断
- 明确当前三类关键缺口
- 给出暂不优先补的方向
- 给出下一步最该补的 3 类材料和阅读顺序
- 更新 `wiki/INDEX.md`

## [2026-04-09] ingest | Attention Is All You Need

处理 `raw/sources/1706.03762v7/1706.03762v7.md`，将 Transformer 原始论文正式纳入知识库：

- 新建资料摘要页 `wiki/sources/attention-is-all-you-need.md`
- 更新概念页 `wiki/concepts/transformers.md`
- 更新资料页 `wiki/sources/the-annotated-transformer.md`
- 更新 `outputs/rnn-transformer-research-decision-memo-2026-04-09.md`
- 更新 `wiki/INDEX.md`

## [2026-04-09] ingest | Neural Machine Translation by Jointly Learning to Align and Translate

处理 `raw/sources/1409.0473v7/1409.0473v7.md`，将 Bahdanau attention 原始论文纳入知识库：

- 新建资料摘要页 `wiki/sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md`
- 新建概念页 `wiki/concepts/attention-mechanisms.md`
- 更新概念页 `wiki/concepts/recurrent-neural-networks.md`
- 更新概念页 `wiki/concepts/sequence-to-sequence-for-sets.md`
- 更新概念页 `wiki/concepts/transformers.md`
- 更新默会知识页 `wiki/notes/cases/tacit-knowledge-on-rnn-to-transformer-transition.md`
- 更新 `outputs/rnn-transformer-research-decision-memo-2026-04-09.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-10] refactor | knowledge-base-agent-skills-layer

为知识库新增一层 repo-local agent skills 操作层：

- 新建 `agent/skills/`，包含 `kb-route`、`kb-ask`、`kb-teach`、`kb-guide`、`kb-locate`、`kb-explain-page`、`kb-synthesize-output`
- 新建 `agent/playbooks/`，补充回答、讲解、阅读路径和沉淀模板
- 新建 `agent/maps/`，补充主题线、高价值页面和 outputs 导航
- 更新 `wiki/INDEX.md` 以纳入新的 agent 层入口

## [2026-04-10] query | knowledge-base-agent-skills-test-report

对第一版知识库 agent skills 做结构校验与 dry run 路由测试：

- 新建 `outputs/knowledge-base-agent-skills-test-report-2026-04-10.md`
- 验证 7 个 skills、4 个 playbooks、3 个 maps 已创建
- 验证 `kb-route -> kb-ask / kb-teach / kb-guide / kb-synthesize-output` 的主要分流
- 修正 `kb-route` 中对产物讲解和混合意图请求的显式路由规则
- 更新 `wiki/INDEX.md`

## [2026-04-10] query | rnn-epistemology

围绕 “RNN 代表了作者什么样的认识论” 生成一份可复用回答，并补齐对应默会知识页：

- 新建 `outputs/rnn-epistemology-2026-04-10.md`
- 新建 `wiki/notes/cases/rnn-as-epistemology.md`
- 将 Karpathy 的 RNN 文章解读为一种过程性认识论与“预测即理解”的模型观
- 更新 `wiki/INDEX.md`

## [2026-04-10] refactor | install-project-local-codex-skills

将知识库 agent skills 局部安装到当前项目的 Codex 技能目录：

- 新建 `.codex/skills/`
- 将 `agent/skills/` 下 7 个知识库技能复制到 `.codex/skills/`
- 验证当前项目可发现 `kb-route`、`kb-ask`、`kb-teach`、`kb-guide`、`kb-locate`、`kb-explain-page`、`kb-synthesize-output`
- 更新 `wiki/INDEX.md`

## [2026-04-10] refactor | add-kb-wiki-first-entry-skill

补充当前仓库的知识库入口 skill：

- 新建 `agent/skills/kb-wiki-first/SKILL.md`
- 新建 `.codex/skills/kb-wiki-first/SKILL.md`
- 明确当前仓库的 `wiki-first` 知识任务顺序与 `kb-route` 默认路由
- 更新 `wiki/INDEX.md`

## [2026-04-10] refactor | add-kb-search-tooling

为知识库 skills 补充 repo-local 快速检索工具与工具使用约定：

- 新建 `scripts/kb`
- 提供 `index`、`files`、`search`、`outputs` 四种检索入口
- 更新 `kb-locate` 与 `kb-wiki-first`，要求优先使用 `scripts/kb`

- 将“可并行窄搜索”写入项目级 `.codex/skills/` 对应技能
- 更新 `wiki/INDEX.md`

## [2026-04-10] refactor | add-kb-related-lookup

为知识库讲解与导航技能补充页面反查工具：

- 为 `scripts/kb` 新增 `related <page-path>` 子命令
- 用 `[[slug]]`、路径引用与标题近似匹配反查相关 pages 与 outputs
- 更新 `kb-teach`、`kb-guide`、`kb-explain-page` 及项目级 `.codex/skills/` 对应技能
- 更新 `wiki/INDEX.md`

## [2026-04-10] query | llm-agents-and-harness-engineering

围绕“如何利用 LLM 的特性开发 agents，以及 harness 工程需要注意什么”生成一份工程指南，并沉淀为默会知识框架：

- 新建 `outputs/llm-agents-and-harness-engineering-2026-04-10.md`
- 新建 `wiki/notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md`
- 结合 OpenAI 与 Anthropic 的官方资料，区分 LLM 适合承担的局部决策能力与 harness 必须接管的机械可靠性
- 更新 `wiki/INDEX.md`

## [2026-04-10] query | agent-harness-minimum-architecture

在 agent 与 harness 原则页基础上，进一步沉淀一个最小可实现的工程蓝图：

- 新建 `outputs/agent-harness-minimum-architecture-2026-04-10.md`
- 新建 `wiki/notes/frameworks/agent-harness-minimum-architecture.md`
- 将最小 agent harness 拆成 task input、agent loop、tool runtime、state store、approval gate、trace logger、evaluator 七个部件
- 更新 `wiki/INDEX.md`

## [2026-04-10] ingest | Deep Residual Learning for Image Recognition

处理 `raw/sources/1512.03385v1/1512.03385v1.md`，将 ResNet 原始论文纳入知识库：

- 新建资料摘要页 `wiki/sources/deep-residual-learning-for-image-recognition.md`
- 新建概念页 `wiki/concepts/residual-networks.md`
- 更新框架页 `wiki/notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-10] ingest | Highway Networks

处理 `raw/sources/1505.00387v2/1505.00387v2.md`，将 Highway Networks 论文纳入知识库：

- 新建资料摘要页 `wiki/sources/highway-networks.md`
- 新建概念页 `wiki/concepts/highway-networks.md`
- 更新概念页 `wiki/concepts/residual-networks.md`
- 更新框架页 `wiki/notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-10] query | highway-networks-vs-resnet

在已有 Highway Networks 与 ResNet 材料基础上，补一层桥梁型默会知识：

- 新建 `outputs/highway-networks-vs-resnet-2026-04-10.md`
- 新建 `wiki/notes/cases/highway-networks-to-resnet-transition.md`
- 将两者的差异压缩为“受控信息流” vs “默认直通 + 增量修正”
- 更新 `wiki/INDEX.md`

## [2026-04-11] ingest | Multi-Scale Context Aggregation by Dilated Convolutions

处理 `raw/sources/1511.07122v3/1511.07122v3.md`，将 dilated convolutions 论文纳入知识库：

- 新建资料摘要页 `wiki/sources/multi-scale-context-aggregation-by-dilated-convolutions.md`
- 新建概念页 `wiki/concepts/dilated-convolutions.md`
- 更新框架页 `wiki/notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-11] query | dense-prediction-vs-classification-architecture

在 dilated convolutions 材料基础上，补一层任务结构驱动的架构判断：

- 新建 `outputs/dense-prediction-vs-classification-architecture-2026-04-11.md`
- 新建 `wiki/notes/cases/dense-prediction-vs-classification-architecture.md`
- 将 dense prediction 与 classification 的架构差异压缩成“任务如何消费空间信息”的判断框架
- 更新 `wiki/INDEX.md`

## [2026-04-11] query | vision-architecture-next-research-directions

在 Highway、ResNet 与 Dilated Convolutions 三条材料基础上，整理视觉架构分支的缺口与下一步阅读顺序：

- 新建 `outputs/vision-architecture-next-research-directions-2026-04-11.md`
- 新建 `wiki/notes/cases/vision-architecture-branching-points.md`
- 将当前视觉材料拆成“深层可训练性”与“dense prediction 结构”两条问题线
- 更新 `wiki/INDEX.md`

## [2026-04-11] refactor | autonomous-handoff-ops-layer

为当前知识库新增一层面向 Codex 长时间自主运行的 ops 结构：

- 新建 `ops/charter.md`
- 新建 `ops/workboard.md`
- 新建 `ops/runbook.md`
- 新建 `ops/handoff.md`
- 新建 `agent/skills/kb-autonomous-run/SKILL.md`
- 新建 `.codex/skills/kb-autonomous-run/SKILL.md`
- 将自然停止点定义为“验证通过且阶段闭环”而不是“小任务完成”
- 更新 `wiki/INDEX.md`

## [2026-04-11] ingest | ImageNet Classification with Deep Convolutional Neural Networks

处理 `raw/sources/NIPS-2012-imagenet-classification-with-deep-convolutional-neural-networks-Paper/NIPS-2012-imagenet-classification-with-deep-convolutional-neural-networks-Paper.md`，将 AlexNet 原始论文纳入知识库：

- 新建资料摘要页 `wiki/sources/imagenet-classification-with-deep-convolutional-neural-networks.md`
- 新建概念页 `wiki/concepts/alexnet.md`
- 新建案例页 `wiki/notes/cases/alexnet-as-scaling-breakthrough.md`
- 更新 `outputs/vision-architecture-next-research-directions-2026-04-11.md`
- 更新 `wiki/notes/cases/vision-architecture-branching-points.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-11] ingest | ToolLLM: Facilitating Large Language Models to Master 16000+ Real-World APIs

处理 `raw/sources/2307.16789v2/2307.16789v2.md`，将 ToolLLM 论文纳入知识库：

- 新建资料摘要页 `wiki/sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md`
- 新建概念页 `wiki/concepts/tool-use-in-llms.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-11] refactor | harden-autonomous-run-against-status-stalls

针对自主运行层容易在“状态汇报点”停住的问题，强化自动运行协议：

- 更新上游仓库 `autonomous-handoff-ops` 中的 `kb-autonomous-run` skill
- 更新上游模板 `ops/runbook.md` 与 `ops/charter.md`
- 明确规定“进度汇报不是停止条件”
- 明确规定“若无阻塞或自然交接点，状态更新后必须继续执行”
- 同步更新当前知识库的 `ops/` 层与项目本地 `kb-autonomous-run`

## [2026-04-11] ingest | Large Language Models as Tool Makers

处理 `raw/sources/2305.17126v2/2305.17126v2.md`，将 LATM 论文纳入知识库：

- 新建资料摘要页 `wiki/sources/large-language-models-as-tool-makers.md`
- 更新概念页 `wiki/concepts/tool-use-in-llms.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-11] ingest | CREATOR: Tool Creation for Disentangling Abstract and Concrete Reasoning of Large Language Models

处理 `raw/sources/2305.14318v3/2305.14318v3.md`，将 CREATOR 论文纳入知识库：

- 新建资料摘要页 `wiki/sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md`
- 更新概念页 `wiki/concepts/tool-use-in-llms.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-11] ingest | An Approach for API Synthesis Using Large Language Models

处理 `raw/sources/2502.15246v1/2502.15246v1.md`，将 API synthesis 论文纳入知识库：

- 新建资料摘要页 `wiki/sources/an-approach-for-api-synthesis-using-large-language-models.md`
- 更新概念页 `wiki/concepts/tool-use-in-llms.md`
- 更新案例页 `wiki/notes/cases/tool-use-tool-making-tool-library-branch.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-11] ingest | ToolLibGen: Scalable Automatic Tool Creation and Aggregation for LLM Reasoning

处理 `raw/sources/2510.07768v1/2510.07768v1.md`，将 ToolLibGen 论文纳入知识库：

- 新建资料摘要页 `wiki/sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md`
- 更新概念页 `wiki/concepts/tool-use-in-llms.md`
- 新建案例页 `wiki/notes/cases/tool-use-tool-making-tool-library-branch.md`
- 新建输出页 `outputs/tool-use-tool-making-tool-library-2026-04-11.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-11] query | aggregate-atomic-cli-commands-for-agents

围绕“如何把原子化 CLI 命令聚合和组装给 agent 使用”生成一份设计指南，并沉淀成通用框架：

- 新建 `outputs/how-to-aggregate-atomic-cli-commands-for-agents-2026-04-11.md`
- 新建 `wiki/notes/frameworks/how-to-aggregate-atomic-cli-commands-for-agents.md`
- 结合 ToolLLM、LATM 和 ToolLibGen，总结从原子命令到任务工具再到工具库的演化范式
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | planning-and-upskilling-agents-with-atomic-cli-tools

围绕“agent 应该怎么规划原子化 CLI 的使用，以及怎么提升使用能力”生成一份更直接的设计指南，并沉淀成框架页：

- 新建 `outputs/planning-and-upskilling-agents-with-atomic-cli-tools-2026-04-13.md`
- 新建 `wiki/notes/frameworks/how-agents-should-plan-and-improve-atomic-cli-usage.md`
- 将原子命令、任务门面、maker-user 分层、库化聚合四层组织成一条能力演化线
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | tool-paper-structure-matrix

围绕 6 篇与 tool 相关的材料生成结构化对照表：

- 新建 `outputs/tool-paper-structure-matrix-2026-04-13.md`
- 新建 `wiki/notes/frameworks/tool-paper-comparison-matrix.md`
- 按 `tool use`、`tool making`、`tool library`、`api synthesis`、`evaluation`、`serving` 六维比较各篇材料
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | five-patterns-and-how-to-apply-for-atomic-cli-agents

围绕 `how-agents-should-plan-and-improve-atomic-cli-usage` 中的 five patterns 和 how to apply，生成一份更细致的人类友好型架构与教学指南：

- 新建 `outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md`
- 将 Atomic Call、Task Facade、Search-Based Planning、Maker-User Split、Library Aggregation 五种模式逐层展开
- 明确把已有 tool 论文作为论据支撑
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | how-the-tool-papers-actually-implement-their-systems

围绕 tool 主线材料生成一份更工程化的实施说明：

- 新建 `outputs/how-the-tool-papers-actually-implement-their-systems-2026-04-13.md`
- 逐篇解释 ToolLLM、CREATOR、LATM、ToolLibGen 与 API synthesis 论文的系统构建方式
- 从设计、技术和构建流程角度补足 five patterns 指南的论文细节
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | cli-tool-system-design-from-tool-papers

围绕“另一个项目里已经有很多 CLI，agent 该怎么优化检索与调用”生成一份更落地的设计映射：

- 新建 `outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md`
- 将 ToolLLM、CREATOR、LATM、ToolLibGen、API synthesis 的工程做法映射成 CLI 项目的多层工具架构
- 明确工具语料层、检索层、规划层、执行层、校验层和资产层的设计
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | tool-governance-layer-for-agentic-knowledge-bases

基于 `outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md` 提炼知识库设计层面的长期结论：

- 新建 `wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md`
- 将 five patterns 映射成当前知识库的 `atomic / facade / planning / governance` 四层工具流
- 明确 `scripts/kb`、`agent/skills/` 与 `ops/` 在知识库里的分层职责
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-13] query | refresh-cli-tool-system-design-mapping

更新 `outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md` 的映射版，使其从泛化 CLI 项目进一步落到当前知识库仓库：

- 补充当前仓库的 `atomic / facade / planning / governance` 四层映射
- 明确 `scripts/kb`、`agent/skills/` 与 `ops/` 在知识库设计中的不同职责
- 增加“更新知识库设计时应先判断 facade、planning 还是 governance”的动作顺序

## [2026-04-13] query | promote-outputs-into-frameworks-or-workflows

将“哪些 output 应进一步沉淀为知识库长期组成部分”写成正式 workflow：

- 新建 `wiki/notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md`
- 定义 `outputs`、`frameworks`、`workflows`、`concepts` 四种去向的判定边界
- 补充 output 升格为 framework 或 workflow 的执行流程
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | validate-knowledge-base-agent-skills-workflow

将 `knowledge-base-agent-skills-test-report` 从一次性测试产物提升为可复用 workflow：

- 新建 `wiki/notes/workflows/how-to-validate-knowledge-base-agent-skills.md`
- 将知识库技能层验证拆成静态结构校验、dry run 路由测试和真实回合验证三步
- 明确最小测试集、通过标准和常见误区
- 更新 `wiki/INDEX.md`

## [2026-04-13] refactor | backfill-missing-output-index-entry

回填此前漏收录的视觉分支 output：

- 将 `outputs/why-identity-mappings-is-the-next-resnet-paper-2026-04-11.md` 加入 `wiki/INDEX.md`
- 保持 `outputs/`、`wiki/notes/cases/` 与视觉分支记录的一致性

## [2026-04-13] query | evaluation-and-serving-in-tool-agent-systems

从 `tool-paper-structure-matrix` 等已有产物中提炼一页新的系统层 framework：

- 新建 `wiki/notes/frameworks/how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md`
- 将 `evaluation` 与 `serving` 从 tool 论文对照表中提升为独立判断框架
- 明确它们不是工具系统的尾部配件，而是系统能力与长期运行结构的一部分
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | how-to-read-a-tool-paper-for-system-construction

将 `how-the-tool-papers-actually-implement-their-systems` 中的稳定阅读方法提升为新的 framework：

- 新建 `wiki/notes/frameworks/how-to-read-a-tool-paper-for-system-construction.md`
- 将 tool 论文阅读聚焦到系统部件、分工、瓶颈层、evaluation 与 serving 位置
- 更新 `wiki/notes/frameworks/research-reading-and-decision-stack.md`，补入 tool/system 论文的专用阅读入口
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | output-promotion-audit

对当前 `outputs/` 做一轮系统性分类审计：

- 新建 `outputs/output-promotion-audit-2026-04-13.md`
- 将现有 outputs 划分为 `已升格`、`部分升格`、`保留 output`
- 明确每个已升格或部分升格产物对应的 `framework`、`workflow` 或 `case`
- 更新 `wiki/INDEX.md`

## [2026-04-13] refactor | add-source-trace-for-partially-promoted-outputs

为 `部分升格` 的 output 及其对应 wiki 页面补充显式回链：

- 给 `outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md` 增加 `Source Trace`
- 给 `outputs/highway-networks-vs-resnet-2026-04-10.md` 增加 `Source Trace`
- 给 `wiki/notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md` 补充上游 output 记录
- 给 `wiki/notes/cases/highway-networks-to-resnet-transition.md` 补充上游 output 记录

## [2026-04-13] query | how-to-write-a-stage-research-decision-memo

将 `next-research-directions` / `research-decision-memo` 类产物中的稳定写法提升为 workflow：

- 新建 `wiki/notes/workflows/how-to-write-a-stage-research-decision-memo.md`
- 将阶段研究 memo 的用途、结构、写作流程和质量标准固定下来
- 以 RNN 和视觉分支的现有 memo 作为上游来源
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | how-to-aggregate-atomic-cli-after-atomization

围绕“CLI 原子化之后如何聚合”撰写一份面向实践的独立文档：

- 新建 `outputs/how-to-aggregate-atomic-cli-after-atomization-2026-04-13.md`
- 将原子层、任务门面层、规划层和工具治理层压成一条清晰的落地路径
- 明确哪些命令该聚合、哪些不该急着聚合，以及最稳的实施顺序
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | atomic-cli-aggregation-derived-versions

基于主文档再生成两份衍生版：

- 新建 `outputs/atomic-cli-aggregation-for-managers-and-architects-2026-04-13.md`
- 新建 `outputs/atomic-cli-aggregation-engineering-checklist-2026-04-13.md`
- 将同一主题分别改写成管理/架构决策版与工程执行 checklist 版
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | atomic-cli-aggregation-reading-pack

将三份 CLI 原子化聚合文档整理成一个可分发的阅读包首页：

- 新建 `outputs/atomic-cli-aggregation-reading-pack-2026-04-13.md`
- 按角色说明总览版、管理版、工程版各自适用对象与阅读顺序
- 补充最短分发建议，方便后续直接转发给不同角色
- 更新 `wiki/INDEX.md`

## [2026-04-13] ingest | harness-engineering-batch-1

对新加入 `raw/inbox/` 的 harness 相关资料做第一批正式入库：

- 新建 4 个资料摘要页：
  - `wiki/sources/harness-engineering-for-coding-agent-users.md`
  - `wiki/sources/harness-design-for-long-running-application-development.md`
  - `wiki/sources/harness-engineering-exploiting-codex-in-the-age-of-agents.md`
  - `wiki/sources/stripe-minions-ai-powered-developer-productivity.md`
- 新建概念页 `wiki/concepts/agent-harness-engineering.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-13] ingest | harness-engineering-batch-2

对同一批 harness 资料做第二轮知识提炼：

- 新建资料摘要页 `wiki/sources/improving-deep-agents-with-harness-engineering.md`
- 新建 framework 页：
  - `wiki/notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md`
  - `wiki/notes/frameworks/how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops.md`
- 更新 `wiki/concepts/agent-harness-engineering.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-13] ingest | harness-engineering-batch-3

继续补齐长时运行 harness 主题：

- 新建 framework 页 `wiki/notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md`
- 将 Anthropic 的长时运行 harness 资料与当前仓库 `ops/runbook` / `ops/handoff` 协议对齐
- 更新 `wiki/concepts/agent-harness-engineering.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-13] ingest | harness-engineering-batch-4

继续补齐 harness 主题的工业案例层：

- 新建案例页 `wiki/notes/cases/stripe-minions-as-infrastructure-first-agent-system.md`
- 将 Stripe Minions 解读为“deterministic infrastructure first”的 agent scale 案例
- 更新 `wiki/concepts/agent-harness-engineering.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-04-13] query | harness-engineering-implications-for-this-knowledge-base

围绕这批 harness 材料生成一份面向当前仓库设计的综合 memo：

- 新建 `outputs/harness-engineering-implications-for-this-knowledge-base-2026-04-13.md`
- 将 concept / frameworks / case 的判断压缩成对当前知识库结构的具体映射
- 明确 knowledge layer、feedforward layer、feedback layer、long-running control layer 的分工
- 给出后续仓库设计的优先级建议
- 更新 `wiki/INDEX.md`

## [2026-04-14] lint | implicit-conventions-audit

对当前仓库里已存在但分散的约定做一轮总览盘点：

- 新建 `outputs/implicit-conventions-audit-2026-04-14.md`
- 将约定分成知识查询、自主运行、沉淀升格、工具治理四类
- 区分哪些已显式写明、哪些仍属隐性、哪些边界不清
- 给出后续优先升格成 guide 的顺序
- 更新 `wiki/INDEX.md`

## [2026-04-14] refactor | route-knowledge-queries-guide

根据隐性约定盘点，优先将知识查询规则收束成正式 guide：

- 新建 `wiki/notes/workflows/how-to-route-knowledge-queries-in-this-repo.md`
- 明确知识查询在 `concepts`、`notes`、`outputs` 与 `raw` 之间的默认路由顺序
- 区分何时先看 `frameworks`、何时先看 `cases`、何时先看 `outputs`
- 更新 `wiki/INDEX.md`

## [2026-04-14] refactor | partially-promoted-outputs-guide

根据隐性约定盘点，继续将“部分升格 output”管理方式收束成正式 guide：

- 新建 `wiki/notes/workflows/how-to-manage-partially-promoted-outputs.md`
- 定义 `partially promoted outputs` 的判定条件与保留理由
- 明确 output 与 wiki 页之间应如何做双向 `Source Trace`
- 更新 `wiki/INDEX.md`

## [2026-04-14] refactor | classify-repo-rules-guide

根据隐性约定盘点，继续将仓库规则对象的归类方式收束成正式 guide：

- 新建 `wiki/notes/workflows/how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md`
- 将当前仓库规则对象分成 `guide / sensor / facade / protocol`
- 明确不同类型对象分别适合落在文档、skill、script 还是 `ops/`
- 更新 `wiki/INDEX.md`

## [2026-04-14] refactor | apply-ops-protocol-outside-autonomous-runs-guide

根据隐性约定盘点，继续将 `ops` 协议的适用边界收束成正式 guide：

- 新建 `wiki/notes/workflows/how-to-apply-ops-protocol-outside-autonomous-runs.md`
- 区分 full ops protocol 与 general quality rules
- 明确哪些规则只适用于 phase-based autonomous run，哪些规则已值得外溢到普通工作
- 更新 `wiki/INDEX.md`

## [2026-04-14] lint | rule-overlap-and-thinning-audit

对入口层规则与 guide 层规则做一轮减重审计：

- 新建 `outputs/rule-overlap-and-thinning-audit-2026-04-14.md`
- 盘点 `AGENTS.md`、`README.md`、`kb-wiki-first` 与 4 个 workflow guides 的规则重叠
- 区分哪些规则应留在入口层，哪些规则应下沉到 guide 层
- 给出后续避免入口层重新膨胀的分层建议
- 更新 `wiki/INDEX.md`

## [2026-04-14] refactor | thin-entry-layer-rules

根据规则重叠审计，对入口层规则做最轻量减重：

- 在 `README.md` 明确更细规则统一见 `wiki/notes/workflows/`
- 在 `AGENTS.md` 明确其只保留总原则，细粒度决策树以下沉 guides 为准
- 保持 `kb-wiki-first` 为最小查询顺序入口，不继续加细路由

## [2026-04-14] refactor | refresh-autonomous-run-context

更新自动化运行仓库状态，使其与当前真实阶段一致：

- 将 `ops/workboard.md` 从旧的 tool branch 切换到新的 `knowledge-base-governance-consolidation` phase
- 更新 `ops/handoff.md`，反映当前入口层减重、workflow 索引和治理收束状态
- 更新 `wiki/INDEX.md` 顶部日期与 Core 条目日期
- 将 `ops/handoff.md` 的类型调整为 `decision-required`，反映新 phase 已切换但尚未完整执行

## [2026-04-14] refactor | compress-ops-feedback-path

压缩当前 autonomous-run 的反馈路径，同时保留兼容性：

- 新建 `scripts/ops-gate`，统一批次检查与停机检查两个 gate
- 将 `scripts/ops-check-handoff-readiness` 与 `scripts/ops-verify-continuation` 改成兼容包装层
- 更新 `ops/runbook.md`，改为使用 `scripts/ops-gate <project-root> batch|stop`
- 更新 `agent/skills/kb-autonomous-run/SKILL.md`，改为引用统一 gate

## [2026-04-14] refactor | clarify-verification-layers

在 `ops/runbook.md` 中补充任务级验证与运行级 gate 的区别：

- 明确 workboard 的 verification method 属于 task-level verification
- 明确 `scripts/ops-gate <project-root> batch|stop` 属于 run-level gate
- 避免后续把 gate 误当成具体 work item 已验证的证据

## [2026-04-14] refactor | workflow-index

为 `wiki/notes/workflows/` 增加一个总索引入口：

- 新建 `wiki/notes/workflows/index.md`
- 按查询、升格、研究推进、协议验证、运行治理、资料预处理分组 workflow
- 增加最短阅读路径，减少 workflow 页自身的分散感
- 更新 `wiki/INDEX.md`

## [2026-04-14] query | harness-engineering-practice-report-and-component-rules

围绕 harness 工程撰写一份面向实践的综合报告：

- 新建 `outputs/harness-engineering-practice-report-and-component-rules-2026-04-14.md`
- 将 harness 拆成 guide、tool/facade、sensor、state/handoff、protocol 五层
- 系统列出每层可有哪些组件与规则设计
- 给出不同场景下的组件重点和最小可落地方案
- 更新 `wiki/INDEX.md`

## [2026-04-14] query | harness-engineering-implementation-checklist

基于实践报告再生成一个工程实施 checklist 版：

- 新建 `outputs/harness-engineering-implementation-checklist-2026-04-14.md`
- 将 harness 拆成 guide、tool/facade、sensor、state/handoff、protocol 五层检查项
- 补充推荐落地顺序、验收标准和常见故障排查
- 更新 `wiki/INDEX.md`

## [2026-04-16] ingest | Identity Mappings in Deep Residual Networks

处理 `raw/inbox/1603.05027v3.pdf`，将 ResNet 的 follow-up 论文纳入知识库：

- 新建资料摘要页 `wiki/sources/identity-mappings-in-deep-residual-networks.md`
- 更新概念页 `wiki/concepts/residual-networks.md`
- 更新默会知识页 `wiki/notes/cases/why-identity-mappings-is-the-next-resnet-step.md`
- 更新视觉分支页 `wiki/notes/cases/vision-architecture-branching-points.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-16] ingest | Variational Lossy Autoencoder

处理 `raw/inbox/1611.02731v2.pdf`，将 VAE 相关新主题纳入知识库：

- 新建资料摘要页 `wiki/sources/variational-lossy-autoencoder.md`
- 新建概念页 `wiki/concepts/variational-autoencoders.md`
- 更新 `wiki/INDEX.md`
- 更新 `wiki/overview.md`

## [2026-04-16] query | decoder-strength-and-latent-usefulness-in-vaes

围绕 VLAE 补充一页可迁移的默会知识：

- 新建案例页 `wiki/notes/cases/how-to-think-about-decoder-strength-and-latent-usefulness-in-vaes.md`
- 将“强 decoder 导致 latent 无用”的常见说法改写成“关键在信息分工”的判断框架
- 更新 `wiki/concepts/variational-autoencoders.md`
- 更新 `wiki/INDEX.md`

## [2026-04-16] query | vae-next-research-directions

基于当前 VLAE 主题线生成一份下一阶段研究方向 memo：

- 新建 `outputs/vae-next-research-directions-2026-04-16.md`
- 压缩当前最稳判断、关键缺口与推荐补的论文顺序
- 明确当前最优 next step 是优先补 posterior collapse / latent collapse 代表材料
- 更新 `wiki/INDEX.md`

## [2026-04-16] query | vae-candidate-papers-and-reading-order

将 VAE 分支的下一步补资料方向进一步具体化：

- 新建 `outputs/vae-candidate-papers-and-reading-order-2026-04-16.md`
- 将 posterior collapse、beta-VAE 与 hierarchical VAE 三条方向具体化成候选论文清单
- 明确当前最推荐先补的是 `Lagging Inference Networks and Posterior Collapse in Variational Autoencoders`
- 更新 `wiki/INDEX.md`

## [2026-04-16] query | vae-free-clustering-analysis

围绕当前 VAE 分支做一轮按问题链的自由聚类：

- 新建 `outputs/vae-free-clustering-analysis-2026-04-16.md`
- 将当前主题线拆成 collapse、shaping、hierarchy、stabilization 四簇
- 明确 `VLAE` 当前位于 collapse 与 shaping 之间的桥梁位置
- 更新 `wiki/INDEX.md`

## [2026-04-16] query | map-vae-papers-by-latent-allocation-problem

将 VAE 分支的自由聚类进一步沉淀成可复用框架：

- 新建 `wiki/notes/frameworks/how-to-map-vae-papers-by-latent-allocation-problem.md`
- 将 VAE 论文按 collapse、shaping、hierarchy、stabilization 四类问题进行路由
- 明确新论文进入时应先按问题簇归类，再决定阅读顺序
- 更新 `wiki/INDEX.md`

## [2026-04-16] query | vae-reading-path

为当前 VAE 分支补一个最短阅读入口：

- 新建 `outputs/vae-reading-path-2026-04-16.md`
- 将当前 source、concept、case、framework 与 next-step outputs 串成最短阅读顺序
- 明确读完后的默认下一步是补 posterior collapse 代表材料
- 更新 `wiki/INDEX.md`

## [2026-04-16] query | vae-target-paper-checklist

为当前 VAE 分支补一份可直接收文件的目标清单：

- 新建 `outputs/vae-target-paper-checklist-2026-04-16.md`
- 将下一步最值得补的论文具体化成标题、标识与稳定入口
- 明确当前最优先投喂的是 `Lagging Inference Networks and Posterior Collapse in Variational Autoencoders`
- 更新 `wiki/INDEX.md`

## [2026-04-16] ingest | Relational recurrent neural networks

处理 `raw/inbox/1806.01822v2.pdf`，将一篇 RNN / relational reasoning 论文纳入知识库：

- 新建资料摘要页 `wiki/sources/relational-recurrent-neural-networks.md`
- 新建概念页 `wiki/concepts/relational-memory-core.md`
- 更新概念页 `wiki/concepts/recurrent-neural-networks.md`
- 更新 `wiki/overview.md`
- 更新 `wiki/INDEX.md`

## [2026-05-05] refactor | rotate-autonomous-phase-to-agent-tool-making-ingest

收口已完成的 governance phase，并为下一条 ingest / research 分支准备新的 autonomous 入口：

- 将 `ops/handoff.md` 从 `decision-required` 收口为 `phase-complete`
- 记录 `knowledge-base-governance-consolidation` 已通过 `scripts/ops-phase-status .` 的全部检查
- 不直接切换 active `ops/workboard.md`，而是在 handoff 中明确下一阶段为 `agent-tool-making-ingest-branch`
- 明确下一阶段首篇待 ingest 资料为 `raw/inbox/2502.11705v2.pdf`（`LLM Agents Making Agent Tools`）
- 更新 `wiki/INDEX.md`

## [2026-05-05] refactor | strengthen-ingest-query-lint-update-contract

强化知识库四种核心模式的入口定义与 workflow 边界：

- 更新 `AGENTS.md`，显式加入 `Ingest / Query / Lint / Update` 四种模式
- 更新 `README.md`，强化提炼优先、双路查询、90 天过期检查与增量更新原则
- 新建 `wiki/notes/workflows/how-to-run-ingest-query-lint-update-in-this-repo.md`
- 更新 `wiki/notes/workflows/index.md`
- 更新 `wiki/INDEX.md`

## [2026-05-05] refactor | add-kb-lint-health-report

把 `Lint` 从文档规则升级为可执行能力：

- 扩展 `scripts/kb`，新增 `scripts/kb lint`
- 让 lint 扫描断链、超过 90 天未更新页面与未登记到 `wiki/INDEX.md` 的孤儿页
- 默认输出 `outputs/wiki-health-report-YYYY-MM-DD.md`
- 更新 `README.md`、workflow 文档与 `wiki/INDEX.md`
