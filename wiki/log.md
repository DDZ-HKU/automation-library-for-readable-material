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
