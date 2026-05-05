# INDEX

最近更新：2026-05-05

## Core

- [overview.md](overview.md) - 当前知识库的范围、目标与主要结构。更新：2026-04-16
- [log.md](log.md) - 知识库演化日志。更新：2026-05-05

## Agent Layer

- [../ops/charter.md](../ops/charter.md) - 自主运行层的长期宪章，定义有价值工作、质量边界与必须交接的人类决策。更新：2026-04-11
- [../ops/workboard.md](../ops/workboard.md) - 自主运行层的当前阶段工作板与验证驱动停止条件。更新：2026-05-05
- [../ops/runbook.md](../ops/runbook.md) - Codex 长时间运行直到自然交接点的执行协议。更新：2026-04-11
- [../ops/handoff.md](../ops/handoff.md) - 最新一次自主运行交接状态。更新：2026-05-05
- [../agent/skills/kb-autonomous-run/SKILL.md](../agent/skills/kb-autonomous-run/SKILL.md) - 让 Codex 基于 ops 层连续运行直到自然交接点的 skill。更新：2026-04-11
- [../agent/skills/kb-wiki-first/SKILL.md](../agent/skills/kb-wiki-first/SKILL.md) - 当前仓库的知识库入口 skill，要求知识任务默认采用 wiki-first 路由。更新：2026-04-10
- [../agent/skills/kb-route/SKILL.md](../agent/skills/kb-route/SKILL.md) - 面向知识库请求的总路由 skill。更新：2026-04-10
- [../agent/skills/kb-ask/SKILL.md](../agent/skills/kb-ask/SKILL.md) - 基于 wiki 和 outputs 的直接问答 skill。更新：2026-04-10
- [../agent/skills/kb-teach/SKILL.md](../agent/skills/kb-teach/SKILL.md) - 围绕知识页和产物做深讲解的 skill。更新：2026-04-10
- [../agent/skills/kb-guide/SKILL.md](../agent/skills/kb-guide/SKILL.md) - 为主题和产物生成最短阅读路径的 skill。更新：2026-04-10
- [../scripts/kb](../scripts/kb) - 供知识库 skills 调用的本地快速检索与 lint 工具，覆盖 index/files/search/outputs/related/lint。更新：2026-05-05
- [../agent/maps/high-value-pages.md](../agent/maps/high-value-pages.md) - 给 agent 优先检索的高价值页面地图。更新：2026-04-10
- [../.codex/skills/kb-wiki-first/SKILL.md](../.codex/skills/kb-wiki-first/SKILL.md) - 安装到当前项目 Codex 本地技能目录的知识库入口 skill。更新：2026-04-10
- [../.codex/skills/kb-autonomous-run/SKILL.md](../.codex/skills/kb-autonomous-run/SKILL.md) - 安装到当前项目 Codex 本地技能目录的自主运行入口 skill。更新：2026-04-11
- [../.codex/skills/kb-route/SKILL.md](../.codex/skills/kb-route/SKILL.md) - 安装到当前项目 Codex 本地技能目录的入口 skill。更新：2026-04-10

## Concepts

- [concepts/llm-wiki.md](concepts/llm-wiki.md) - 以 LLM 维护持久化 wiki 的知识管理模式。更新：2026-04-07，来源：0
- [concepts/agent-harness-engineering.md](concepts/agent-harness-engineering.md) - 围绕状态、环境、反馈、trace、eval 与长时运行协议的 agent harness 工程主题页。更新：2026-04-13，来源：4
- [concepts/complextropy.md](concepts/complextropy.md) - 讨论“熵之外的中间态复杂性”的概念页。更新：2026-04-08，来源：1
- [concepts/recurrent-neural-networks.md](concepts/recurrent-neural-networks.md) - 递归神经网络、LSTM、长程依赖、seq2seq 与训练经验的概念页。更新：2026-04-09，来源：6
- [concepts/tool-use-in-llms.md](concepts/tool-use-in-llms.md) - Tool use 作为 LLM 能力链：检索、规划、执行、反馈与评估的系统化主题页。更新：2026-04-11，来源：1
- [concepts/alexnet.md](concepts/alexnet.md) - AlexNet 如何把大规模数据、GPU、ReLU 与 dropout 组装成视觉深度学习的突破点。更新：2026-04-11，来源：1
- [concepts/variational-autoencoders.md](concepts/variational-autoencoders.md) - VAE 如何在 latent 表征与 decoder 细节建模之间分工，以及为何 lossy latent 可能是有意设计。更新：2026-04-16，来源：1
- [concepts/residual-networks.md](concepts/residual-networks.md) - ResNet 如何通过 residual reformulation 与 shortcut 连接缓解深层网络优化困难，并在后续演化中收敛到更干净的 identity path。更新：2026-04-16，来源：2
- [concepts/relational-memory-core.md](concepts/relational-memory-core.md) - Relational Memory Core 如何把 attention 变成 memory 内部的关系交互算子。更新：2026-04-16，来源：1
- [concepts/highway-networks.md](concepts/highway-networks.md) - Highway Networks 如何通过 gated carry path 让极深网络更可训练。更新：2026-04-10，来源：1
- [concepts/dilated-convolutions.md](concepts/dilated-convolutions.md) - Dilated convolution 如何在 dense prediction 中扩张感受野而不损失分辨率。更新：2026-04-11，来源：1
- [concepts/attention-mechanisms.md](concepts/attention-mechanisms.md) - attention 如何从 RNN 的 soft alignment 补丁演化为主要信息访问机制。更新：2026-04-09，来源：3
- [concepts/sequence-to-sequence-for-sets.md](concepts/sequence-to-sequence-for-sets.md) - seq2seq 如何处理集合输入/输出，以及为什么顺序选择会影响学习。更新：2026-04-09，来源：5
- [concepts/transformers.md](concepts/transformers.md) - Transformer 如何把 attention 从辅助机制推进成主架构。更新：2026-04-09，来源：5
- [concepts/pipeline-parallelism.md](concepts/pipeline-parallelism.md) - 通过 micro-batch 流水线把超大模型切分到多设备训练的系统方法。更新：2026-04-09，来源：1

## Sources

- [sources/the-first-law-of-complexodynamics.md](sources/the-first-law-of-complexodynamics.md) - Aaronson 关于复杂性先升后降现象的理论草图。更新：2026-04-08
- [sources/the-unreasonable-effectiveness-of-recurrent-neural-networks.md](sources/the-unreasonable-effectiveness-of-recurrent-neural-networks.md) - Karpathy 对 RNN/LSTM 与字符级生成建模的经典解释。更新：2026-04-08
- [sources/understanding-lstm-networks.md](sources/understanding-lstm-networks.md) - colah 对 LSTM 长程依赖与门控机制的经典解释。更新：2026-04-08
- [sources/recurrent-neural-network-regularization.md](sources/recurrent-neural-network-regularization.md) - Zaremba 等关于 LSTM dropout 正则化的论文摘要。更新：2026-04-08
- [sources/order-matters-sequence-to-sequence-for-sets.md](sources/order-matters-sequence-to-sequence-for-sets.md) - Vinyals 等关于 seq2seq 在集合输入/输出上扩展及“顺序重要性”的论文摘要。更新：2026-04-09
- [sources/relational-recurrent-neural-networks.md](sources/relational-recurrent-neural-networks.md) - RMC 论文摘要，聚焦 memory 内部的关系交互与 relational reasoning。更新：2026-04-16
- [sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md](sources/toolllm-facilitating-large-language-models-to-master-16000-real-world-apis.md) - ToolLLM 原始论文摘要，聚焦 ToolBench、ToolEval、API 检索与搜索式推理。更新：2026-04-11
- [sources/harness-engineering-for-coding-agent-users.md](sources/harness-engineering-for-coding-agent-users.md) - Thoughtworks 对 coding agent 外层 harness 的边界、guides/sensors 与 harnessability 的系统整理。更新：2026-04-13
- [sources/harness-design-for-long-running-application-development.md](sources/harness-design-for-long-running-application-development.md) - Anthropic 关于长时运行应用开发 harness 的 planner/generator/evaluator 与 handoff 结构。更新：2026-04-13
- [sources/harness-engineering-exploiting-codex-in-the-age-of-agents.md](sources/harness-engineering-exploiting-codex-in-the-age-of-agents.md) - OpenAI 对 agent-first 软件工程中环境、文档与反馈回路的工程实践总结。更新：2026-04-13
- [sources/stripe-minions-ai-powered-developer-productivity.md](sources/stripe-minions-ai-powered-developer-productivity.md) - Stripe Minions 案例，聚焦 devbox、blueprints、curated tools 与分层反馈。更新：2026-04-13
- [sources/improving-deep-agents-with-harness-engineering.md](sources/improving-deep-agents-with-harness-engineering.md) - LangChain 解读链中关于 traces、middleware、自验证与推理预算优化的 harness 经验总结。更新：2026-04-13
- [sources/large-language-models-as-tool-makers.md](sources/large-language-models-as-tool-makers.md) - LATM 原始论文摘要，聚焦 tool making、functional cache 与成本分工。更新：2026-04-11
- [sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md](sources/creator-tool-creation-for-disentangling-abstract-and-concrete-reasoning-of-large-language-models.md) - CREATOR 原始论文摘要，聚焦工具创建与抽象/具体推理解耦。更新：2026-04-11
- [sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md](sources/toollibgen-scalable-automatic-tool-creation-and-aggregation-for-llm-reasoning.md) - ToolLibGen 原始论文摘要，聚焦工具聚类、聚合与结构化库组织。更新：2026-04-11
- [sources/an-approach-for-api-synthesis-using-large-language-models.md](sources/an-approach-for-api-synthesis-using-large-language-models.md) - API synthesis 论文摘要，聚焦输入输出示例驱动的 LLM API 实现综合。更新：2026-04-11
- [sources/imagenet-classification-with-deep-convolutional-neural-networks.md](sources/imagenet-classification-with-deep-convolutional-neural-networks.md) - AlexNet 原始论文摘要，聚焦视觉深度学习的规模化突破。更新：2026-04-11
- [sources/variational-lossy-autoencoder.md](sources/variational-lossy-autoencoder.md) - VLAE 论文摘要，聚焦 lossy latent representation 与 autoregressive decoder 的分工。更新：2026-04-16
- [sources/deep-residual-learning-for-image-recognition.md](sources/deep-residual-learning-for-image-recognition.md) - ResNet 原始论文摘要，聚焦 degradation problem 与 residual reformulation。更新：2026-04-10
- [sources/identity-mappings-in-deep-residual-networks.md](sources/identity-mappings-in-deep-residual-networks.md) - ResNet follow-up 论文摘要，聚焦 identity shortcut、pre-activation 与更干净的信息传播路径。更新：2026-04-16
- [sources/highway-networks.md](sources/highway-networks.md) - Highway Networks 原始扩展摘要，聚焦 gating 机制与极深网络优化。更新：2026-04-10
- [sources/multi-scale-context-aggregation-by-dilated-convolutions.md](sources/multi-scale-context-aggregation-by-dilated-convolutions.md) - Dilated convolution 原始论文摘要，聚焦 dense prediction 的上下文聚合与分辨率保持。更新：2026-04-11
- [sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md](sources/neural-machine-translation-by-jointly-learning-to-align-and-translate.md) - Bahdanau 等提出经典 soft alignment attention 的论文摘要。更新：2026-04-09
- [sources/attention-is-all-you-need.md](sources/attention-is-all-you-need.md) - Transformer 原始论文摘要，明确其对 recurrence 与 convolution 的替代主张。更新：2026-04-09
- [sources/the-annotated-transformer.md](sources/the-annotated-transformer.md) - 对 Transformer 原始论文的注释版实现说明，强调 self-attention 主导的架构转变。更新：2026-04-09
- [sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md](sources/gpipe-easy-scaling-with-micro-batch-pipeline-parallelism.md) - GPipe 如何通过 micro-batch pipeline parallelism 训练超大网络。更新：2026-04-09

## Entities

- 暂无

## Notes

工作流：
- [notes/workflows/index.md](notes/workflows/index.md) - workflow 总索引页，按用途分组并提供最短阅读路径。更新：2026-04-14
- [notes/workflows/pdf-to-markdown-preprocessing.md](notes/workflows/pdf-to-markdown-preprocessing.md) - 本地 `marker` 驱动的 PDF 预处理流程与已验证用法。更新：2026-04-09
- [notes/workflows/how-to-run-ingest-query-lint-update-in-this-repo.md](notes/workflows/how-to-run-ingest-query-lint-update-in-this-repo.md) - 统一定义 `Ingest / Query / Lint / Update` 四种核心模式及其边界。更新：2026-05-05
- [notes/workflows/how-to-route-knowledge-queries-in-this-repo.md](notes/workflows/how-to-route-knowledge-queries-in-this-repo.md) - 规定知识查询时如何在 concepts、notes、outputs 与 raw 之间做稳定路由。更新：2026-04-14
- [notes/workflows/how-to-manage-partially-promoted-outputs.md](notes/workflows/how-to-manage-partially-promoted-outputs.md) - 规定核心结论已进 wiki、但 output 仍保留独特价值时，应如何做部分升格管理与双向回链。更新：2026-04-14
- [notes/workflows/how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md](notes/workflows/how-to-classify-repo-rules-as-guides-sensors-facades-or-protocol.md) - 规定当前仓库的规则对象应如何区分为 guide、sensor、facade 或 protocol。更新：2026-04-14
- [notes/workflows/how-to-apply-ops-protocol-outside-autonomous-runs.md](notes/workflows/how-to-apply-ops-protocol-outside-autonomous-runs.md) - 规定 `ops` 协议在 autonomous run 之外应如何部分继承、而不是生硬套用。更新：2026-04-14
- [notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md](notes/workflows/how-to-promote-outputs-into-frameworks-or-workflows.md) - 定义高价值 outputs 何时应升格为 frameworks 或 workflows 的判定边界与执行流程。更新：2026-04-13
- [notes/workflows/how-to-validate-knowledge-base-agent-skills.md](notes/workflows/how-to-validate-knowledge-base-agent-skills.md) - 规定知识库技能层应如何做静态校验、dry run 路由测试与真实回合验证。更新：2026-04-13
- [notes/workflows/how-to-write-a-stage-research-decision-memo.md](notes/workflows/how-to-write-a-stage-research-decision-memo.md) - 规定阶段研究决策 memo 应如何压缩当前判断、识别缺口并排出下一步阅读顺序。更新：2026-04-13
框架：
- [notes/frameworks/tacit-knowledge-layer.md](notes/frameworks/tacit-knowledge-layer.md) - 知识库中“默会知识层”的目标、边界与标准结构。更新：2026-04-09
- [notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md) - 区分架构、优化和系统问题的通用判断模板。更新：2026-04-09
- [notes/frameworks/how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value.md](notes/frameworks/how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value.md) - 读取模型论文时识别机制、瓶颈与迁移价值的阅读模板。更新：2026-04-09
- [notes/frameworks/how-to-read-a-tool-paper-for-system-construction.md](notes/frameworks/how-to-read-a-tool-paper-for-system-construction.md) - 读取 tool 论文时识别系统部件、分工、瓶颈层与可迁移结构的阅读模板。更新：2026-04-13
- [notes/frameworks/research-reading-and-decision-stack.md](notes/frameworks/research-reading-and-decision-stack.md) - 将问题分层、论文阅读与研究决策串成一条完整流程的总导航页。更新：2026-04-09
- [notes/frameworks/how-to-turn-paper-reading-into-research-decisions.md](notes/frameworks/how-to-turn-paper-reading-into-research-decisions.md) - 把论文阅读结果压缩成下一步研究动作的决策模板。更新：2026-04-09
- [notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md) - 区分哪些能力该交给 LLM，哪些稳定性必须由 harness 接管的 agent 工程框架。更新：2026-04-10
- [notes/frameworks/agent-harness-minimum-architecture.md](notes/frameworks/agent-harness-minimum-architecture.md) - 将 agent harness 压缩成最小可实现闭环的工程蓝图。更新：2026-04-10
- [notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md](notes/frameworks/how-to-separate-feedforward-guides-and-feedback-sensors-in-agent-harnesses.md) - 区分事前 guides 与事后 sensors，并按 computational/inferential 拆 agent harness 控制。更新：2026-04-13
- [notes/frameworks/how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops.md](notes/frameworks/how-to-improve-agent-harnesses-with-traces-middleware-and-verification-loops.md) - 解释如何用 traces、middleware 与 verification loop 持续优化 agent harness。更新：2026-04-13
- [notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md](notes/frameworks/how-to-use-context-resets-compaction-and-handoffs-in-long-running-agent-work.md) - 区分 context reset、compaction 与 handoff artifact 在长时运行 agent 中各自解决的问题。更新：2026-04-13
- [notes/frameworks/how-to-aggregate-atomic-cli-commands-for-agents.md](notes/frameworks/how-to-aggregate-atomic-cli-commands-for-agents.md) - 解释如何把原子 CLI 提升成任务工具与工具库的聚合框架。更新：2026-04-11
- [notes/frameworks/how-agents-should-plan-and-improve-atomic-cli-usage.md](notes/frameworks/how-agents-should-plan-and-improve-atomic-cli-usage.md) - 解释 agent 应如何规划原子 CLI 的使用，并沿 use/make/library 路线提升能力。更新：2026-04-13
- [notes/frameworks/how-to-map-vae-papers-by-latent-allocation-problem.md](notes/frameworks/how-to-map-vae-papers-by-latent-allocation-problem.md) - 把 VAE 文献按 collapse、shaping、hierarchy、stabilization 四类 latent allocation 问题来归类。更新：2026-04-16
- [notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md](notes/frameworks/how-to-design-a-tool-governance-layer-for-agentic-knowledge-bases.md) - 将 tool 论文中的五种模式映射成知识库里的 atomic/facade/planning/governance 四层设计。更新：2026-04-13
- [notes/frameworks/how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md](notes/frameworks/how-to-think-about-evaluation-and-serving-in-tool-agent-systems.md) - 解释为什么 evaluation 与 serving 不是工具系统的尾部配件，而是系统能力的一部分。更新：2026-04-13
- [notes/frameworks/tool-paper-comparison-matrix.md](notes/frameworks/tool-paper-comparison-matrix.md) - 按 tool use / making / library / synthesis / evaluation / serving 六维比较工具论文。更新：2026-04-13
案例：
- [notes/cases/tacit-knowledge-on-rnn-to-transformer-transition.md](notes/cases/tacit-knowledge-on-rnn-to-transformer-transition.md) - 用 RNN 到 Transformer 的演化线讲解如何思考、判断和应用模型范式变化。更新：2026-04-09
- [notes/cases/rnn-as-epistemology.md](notes/cases/rnn-as-epistemology.md) - 从 Karpathy 的 RNN 文章抽取其隐含的过程性认识论与“预测即理解”倾向。更新：2026-04-10
- [notes/cases/alexnet-as-scaling-breakthrough.md](notes/cases/alexnet-as-scaling-breakthrough.md) - 将 AlexNet 解释为视觉深度学习的规模化组合断点。更新：2026-04-11
- [notes/cases/tool-use-tool-making-tool-library-branch.md](notes/cases/tool-use-tool-making-tool-library-branch.md) - 将 ToolLLM、LATM 与 ToolLibGen 串成一条从 tool use 到 tool governance 的系统演化线。更新：2026-04-11
- [notes/cases/stripe-minions-as-infrastructure-first-agent-system.md](notes/cases/stripe-minions-as-infrastructure-first-agent-system.md) - 用 Stripe Minions 说明 agent scale 的真正底座是 deterministic infrastructure，而不只是更强 agent。更新：2026-04-13
- [notes/cases/highway-networks-to-resnet-transition.md](notes/cases/highway-networks-to-resnet-transition.md) - 用 Highway Networks 到 ResNet 的过渡线讲解“受控信息流”与“默认直通 + 增量修正”的差异。更新：2026-04-10
- [notes/cases/why-identity-mappings-is-the-next-resnet-step.md](notes/cases/why-identity-mappings-is-the-next-resnet-step.md) - 记录 Identity Mappings 为什么是 residual line 的关键下一步，以及它实际补上的结构规范化。更新：2026-04-16
- [notes/cases/how-to-think-about-decoder-strength-and-latent-usefulness-in-vaes.md](notes/cases/how-to-think-about-decoder-strength-and-latent-usefulness-in-vaes.md) - 用 VLAE 说明强 decoder 与 latent usefulness 的关键不是对抗，而是信息分工。更新：2026-04-16
- [notes/cases/dense-prediction-vs-classification-architecture.md](notes/cases/dense-prediction-vs-classification-architecture.md) - 用 dilated convolutions 说明 dense prediction 如何逼出不同于 classification 的架构判断。更新：2026-04-11
- [notes/cases/vision-architecture-branching-points.md](notes/cases/vision-architecture-branching-points.md) - 将当前视觉材料拆成“深层可训练性”和“dense prediction 结构”两条问题线，并记录 residual line 已补到 Identity/Pre-activation。更新：2026-04-16

## Outputs

- [../outputs/rnn-lstm-phase-summary-2026-04-08.md](../outputs/rnn-lstm-phase-summary-2026-04-08.md) - 基于三份 RNN/LSTM 资料形成的阶段总结。更新：2026-04-08
- [../outputs/rnn-next-research-directions-2026-04-08.md](../outputs/rnn-next-research-directions-2026-04-08.md) - RNN/LSTM 主题下一阶段应补的研究方向与资料计划。更新：2026-04-08
- [../outputs/vae-next-research-directions-2026-04-16.md](../outputs/vae-next-research-directions-2026-04-16.md) - 基于当前 VLAE 主题线形成的下一阶段研究方向与补资料顺序。更新：2026-04-16
- [../outputs/vae-candidate-papers-and-reading-order-2026-04-16.md](../outputs/vae-candidate-papers-and-reading-order-2026-04-16.md) - 将 VAE 分支下一步最值得补的论文具体化成候选清单与阅读顺序。更新：2026-04-16
- [../outputs/vae-free-clustering-analysis-2026-04-16.md](../outputs/vae-free-clustering-analysis-2026-04-16.md) - 按问题链而非按年份对当前 VAE 分支做自由聚类。更新：2026-04-16
- [../outputs/vae-reading-path-2026-04-16.md](../outputs/vae-reading-path-2026-04-16.md) - 给当前 VAE 分支的最短阅读路径与下一步动作。更新：2026-04-16
- [../outputs/vae-target-paper-checklist-2026-04-16.md](../outputs/vae-target-paper-checklist-2026-04-16.md) - 把当前 VAE 分支下一步最该投喂的论文整理成可执行清单。更新：2026-04-16
- [../outputs/rnn-transformer-research-decision-memo-2026-04-09.md](../outputs/rnn-transformer-research-decision-memo-2026-04-09.md) - 基于当前 RNN 到 Transformer 主题线形成的下一阶段研究决策 memo。更新：2026-04-09
- [../outputs/rnn-epistemology-2026-04-10.md](../outputs/rnn-epistemology-2026-04-10.md) - 围绕 Karpathy 的 RNN 文章回答“RNN 代表了作者什么样的认识论”。更新：2026-04-10
- [../outputs/knowledge-base-agent-skills-test-report-2026-04-10.md](../outputs/knowledge-base-agent-skills-test-report-2026-04-10.md) - 第一版知识库 agent skills 的静态校验与 dry run 测试报告。更新：2026-04-10
- [../outputs/llm-agents-and-harness-engineering-2026-04-10.md](../outputs/llm-agents-and-harness-engineering-2026-04-10.md) - 讲解如何利用 LLM 的特性开发 agents，以及 harness 工程的关键边界与常见坑。更新：2026-04-10
- [../outputs/agent-harness-minimum-architecture-2026-04-10.md](../outputs/agent-harness-minimum-architecture-2026-04-10.md) - 将 agent harness 拆成最小闭环组件、状态层和评估层的工程蓝图。更新：2026-04-10
- [../outputs/highway-networks-vs-resnet-2026-04-10.md](../outputs/highway-networks-vs-resnet-2026-04-10.md) - 比较 Highway Networks 与 ResNet 在解决深层网络优化问题时的不同工程哲学。更新：2026-04-10
- [../outputs/dense-prediction-vs-classification-architecture-2026-04-11.md](../outputs/dense-prediction-vs-classification-architecture-2026-04-11.md) - 解释 dense prediction 为什么会逼出不同于 classification 的架构取舍。更新：2026-04-11
- [../outputs/vision-architecture-next-research-directions-2026-04-11.md](../outputs/vision-architecture-next-research-directions-2026-04-11.md) - 当前视觉架构分支的下一步补资料顺序与缺口判断。更新：2026-04-11
- [../outputs/why-identity-mappings-is-the-next-resnet-paper-2026-04-11.md](../outputs/why-identity-mappings-is-the-next-resnet-paper-2026-04-11.md) - 解释为什么当前视觉分支最该补的是 Identity Mappings in Deep Residual Networks。更新：2026-04-11
- [../outputs/tool-use-tool-making-tool-library-2026-04-11.md](../outputs/tool-use-tool-making-tool-library-2026-04-11.md) - 将 ToolLLM、LATM 与 ToolLibGen 压缩成一条工具系统成熟路径。更新：2026-04-11
- [../outputs/how-to-aggregate-atomic-cli-commands-for-agents-2026-04-11.md](../outputs/how-to-aggregate-atomic-cli-commands-for-agents-2026-04-11.md) - 说明原子 CLI 命令如何提升成任务工具与工具库，以及常见聚合范式。更新：2026-04-11
- [../outputs/planning-and-upskilling-agents-with-atomic-cli-tools-2026-04-13.md](../outputs/planning-and-upskilling-agents-with-atomic-cli-tools-2026-04-13.md) - 说明 agent 如何规划原子 CLI 的使用，以及如何持续提升工具使用能力。更新：2026-04-13
- [../outputs/tool-paper-structure-matrix-2026-04-13.md](../outputs/tool-paper-structure-matrix-2026-04-13.md) - 将 6 篇与 tool 相关材料按 use/make/library/synthesis/evaluation/serving 六维对照。更新：2026-04-13
- [../outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md](../outputs/five-patterns-and-how-to-apply-for-atomic-cli-agents-2026-04-13.md) - 对 five patterns 与 how to apply 做面向人类阅读的详细架构和教学展开。更新：2026-04-13
- [../outputs/how-the-tool-papers-actually-implement-their-systems-2026-04-13.md](../outputs/how-the-tool-papers-actually-implement-their-systems-2026-04-13.md) - 逐篇解释 tool 论文在工程上如何实施、用了哪些设计和技术。更新：2026-04-13
- [../outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md](../outputs/cli-tool-system-design-from-tool-papers-2026-04-13.md) - 把 tool 论文的系统实现映射成 CLI 项目的可落地多层工具架构。更新：2026-04-13
- [../outputs/how-to-aggregate-atomic-cli-after-atomization-2026-04-13.md](../outputs/how-to-aggregate-atomic-cli-after-atomization-2026-04-13.md) - 说明 CLI 原子化之后应如何分层聚合、按何种判据聚合、以及如何分阶段落地。更新：2026-04-13
- [../outputs/atomic-cli-aggregation-for-managers-and-architects-2026-04-13.md](../outputs/atomic-cli-aggregation-for-managers-and-architects-2026-04-13.md) - 面向管理者与架构师，解释 CLI 原子化后为何必须继续聚合，以及该如何分层投入。更新：2026-04-13
- [../outputs/atomic-cli-aggregation-engineering-checklist-2026-04-13.md](../outputs/atomic-cli-aggregation-engineering-checklist-2026-04-13.md) - 面向工程执行，给出 CLI 原子化聚合的候选判据、实现方式与落地 checklist。更新：2026-04-13
- [../outputs/atomic-cli-aggregation-reading-pack-2026-04-13.md](../outputs/atomic-cli-aggregation-reading-pack-2026-04-13.md) - 作为三份 CLI 原子化聚合文档的阅读入口，按角色给出阅读顺序和分发建议。更新：2026-04-13
- [../outputs/harness-engineering-implications-for-this-knowledge-base-2026-04-13.md](../outputs/harness-engineering-implications-for-this-knowledge-base-2026-04-13.md) - 综合说明这批 harness 材料对当前知识库/agent 仓库设计的直接含义与下一步重点。更新：2026-04-13
- [../outputs/implicit-conventions-audit-2026-04-14.md](../outputs/implicit-conventions-audit-2026-04-14.md) - 盘点当前仓库分散存在的隐性约定，并给出优先升格成 guide 的顺序。更新：2026-04-14
- [../outputs/rule-overlap-and-thinning-audit-2026-04-14.md](../outputs/rule-overlap-and-thinning-audit-2026-04-14.md) - 盘点 AGENTS、README、skills 与 workflow guides 之间的规则重叠，并提出减重边界。更新：2026-04-14
- [../outputs/harness-engineering-practice-report-and-component-rules-2026-04-14.md](../outputs/harness-engineering-practice-report-and-component-rules-2026-04-14.md) - 总结 harness 工程可有哪些组件层、规则设计与最小可落地方案。更新：2026-04-14
- [../outputs/harness-engineering-implementation-checklist-2026-04-14.md](../outputs/harness-engineering-implementation-checklist-2026-04-14.md) - 面向工程实施，给出 harness 从 guide 到 protocol 的分层检查项、落地顺序与故障排查。更新：2026-04-14
- [../outputs/output-promotion-audit-2026-04-13.md](../outputs/output-promotion-audit-2026-04-13.md) - 审计当前 outputs 中哪些已升格、部分升格，或应继续作为阶段产物保留。更新：2026-04-13
