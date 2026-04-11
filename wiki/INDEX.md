# INDEX

最近更新：2026-04-09

## Core

- [overview.md](overview.md) - 当前知识库的范围、目标与主要结构。更新：2026-04-09
- [log.md](log.md) - 知识库演化日志。更新：2026-04-09

## Agent Layer

- [../ops/charter.md](../ops/charter.md) - 自主运行层的长期宪章，定义有价值工作、质量边界与必须交接的人类决策。更新：2026-04-11
- [../ops/workboard.md](../ops/workboard.md) - 自主运行层的当前阶段工作板与验证驱动停止条件。更新：2026-04-11
- [../ops/runbook.md](../ops/runbook.md) - Codex 长时间运行直到自然交接点的执行协议。更新：2026-04-11
- [../ops/handoff.md](../ops/handoff.md) - 最新一次自主运行交接状态。更新：2026-04-11
- [../agent/skills/kb-autonomous-run/SKILL.md](../agent/skills/kb-autonomous-run/SKILL.md) - 让 Codex 基于 ops 层连续运行直到自然交接点的 skill。更新：2026-04-11
- [../agent/skills/kb-wiki-first/SKILL.md](../agent/skills/kb-wiki-first/SKILL.md) - 当前仓库的知识库入口 skill，要求知识任务默认采用 wiki-first 路由。更新：2026-04-10
- [../agent/skills/kb-route/SKILL.md](../agent/skills/kb-route/SKILL.md) - 面向知识库请求的总路由 skill。更新：2026-04-10
- [../agent/skills/kb-ask/SKILL.md](../agent/skills/kb-ask/SKILL.md) - 基于 wiki 和 outputs 的直接问答 skill。更新：2026-04-10
- [../agent/skills/kb-teach/SKILL.md](../agent/skills/kb-teach/SKILL.md) - 围绕知识页和产物做深讲解的 skill。更新：2026-04-10
- [../agent/skills/kb-guide/SKILL.md](../agent/skills/kb-guide/SKILL.md) - 为主题和产物生成最短阅读路径的 skill。更新：2026-04-10
- [../scripts/kb](../scripts/kb) - 供知识库 skills 调用的本地快速检索工具，覆盖 index/files/search/outputs/related。更新：2026-04-10
- [../agent/maps/high-value-pages.md](../agent/maps/high-value-pages.md) - 给 agent 优先检索的高价值页面地图。更新：2026-04-10
- [../.codex/skills/kb-wiki-first/SKILL.md](../.codex/skills/kb-wiki-first/SKILL.md) - 安装到当前项目 Codex 本地技能目录的知识库入口 skill。更新：2026-04-10
- [../.codex/skills/kb-autonomous-run/SKILL.md](../.codex/skills/kb-autonomous-run/SKILL.md) - 安装到当前项目 Codex 本地技能目录的自主运行入口 skill。更新：2026-04-11
- [../.codex/skills/kb-route/SKILL.md](../.codex/skills/kb-route/SKILL.md) - 安装到当前项目 Codex 本地技能目录的入口 skill。更新：2026-04-10

## Concepts

- [concepts/llm-wiki.md](concepts/llm-wiki.md) - 以 LLM 维护持久化 wiki 的知识管理模式。更新：2026-04-07，来源：0
- [concepts/complextropy.md](concepts/complextropy.md) - 讨论“熵之外的中间态复杂性”的概念页。更新：2026-04-08，来源：1
- [concepts/recurrent-neural-networks.md](concepts/recurrent-neural-networks.md) - 递归神经网络、LSTM、长程依赖、seq2seq 与训练经验的概念页。更新：2026-04-09，来源：6
- [concepts/alexnet.md](concepts/alexnet.md) - AlexNet 如何把大规模数据、GPU、ReLU 与 dropout 组装成视觉深度学习的突破点。更新：2026-04-11，来源：1
- [concepts/residual-networks.md](concepts/residual-networks.md) - ResNet 如何通过 residual reformulation 与 shortcut 连接缓解深层网络优化困难。更新：2026-04-10，来源：1
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
- [sources/imagenet-classification-with-deep-convolutional-neural-networks.md](sources/imagenet-classification-with-deep-convolutional-neural-networks.md) - AlexNet 原始论文摘要，聚焦视觉深度学习的规模化突破。更新：2026-04-11
- [sources/deep-residual-learning-for-image-recognition.md](sources/deep-residual-learning-for-image-recognition.md) - ResNet 原始论文摘要，聚焦 degradation problem 与 residual reformulation。更新：2026-04-10
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
- [notes/workflows/pdf-to-markdown-preprocessing.md](notes/workflows/pdf-to-markdown-preprocessing.md) - 本地 `marker` 驱动的 PDF 预处理流程与已验证用法。更新：2026-04-09
框架：
- [notes/frameworks/tacit-knowledge-layer.md](notes/frameworks/tacit-knowledge-layer.md) - 知识库中“默会知识层”的目标、边界与标准结构。更新：2026-04-09
- [notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md](notes/frameworks/how-to-distinguish-architecture-optimization-and-systems-problems.md) - 区分架构、优化和系统问题的通用判断模板。更新：2026-04-09
- [notes/frameworks/how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value.md](notes/frameworks/how-to-read-a-model-paper-for-mechanism-bottleneck-and-transfer-value.md) - 读取模型论文时识别机制、瓶颈与迁移价值的阅读模板。更新：2026-04-09
- [notes/frameworks/research-reading-and-decision-stack.md](notes/frameworks/research-reading-and-decision-stack.md) - 将问题分层、论文阅读与研究决策串成一条完整流程的总导航页。更新：2026-04-09
- [notes/frameworks/how-to-turn-paper-reading-into-research-decisions.md](notes/frameworks/how-to-turn-paper-reading-into-research-decisions.md) - 把论文阅读结果压缩成下一步研究动作的决策模板。更新：2026-04-09
- [notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md) - 区分哪些能力该交给 LLM，哪些稳定性必须由 harness 接管的 agent 工程框架。更新：2026-04-10
- [notes/frameworks/agent-harness-minimum-architecture.md](notes/frameworks/agent-harness-minimum-architecture.md) - 将 agent harness 压缩成最小可实现闭环的工程蓝图。更新：2026-04-10
案例：
- [notes/cases/tacit-knowledge-on-rnn-to-transformer-transition.md](notes/cases/tacit-knowledge-on-rnn-to-transformer-transition.md) - 用 RNN 到 Transformer 的演化线讲解如何思考、判断和应用模型范式变化。更新：2026-04-09
- [notes/cases/rnn-as-epistemology.md](notes/cases/rnn-as-epistemology.md) - 从 Karpathy 的 RNN 文章抽取其隐含的过程性认识论与“预测即理解”倾向。更新：2026-04-10
- [notes/cases/alexnet-as-scaling-breakthrough.md](notes/cases/alexnet-as-scaling-breakthrough.md) - 将 AlexNet 解释为视觉深度学习的规模化组合断点。更新：2026-04-11
- [notes/cases/highway-networks-to-resnet-transition.md](notes/cases/highway-networks-to-resnet-transition.md) - 用 Highway Networks 到 ResNet 的过渡线讲解“受控信息流”与“默认直通 + 增量修正”的差异。更新：2026-04-10
- [notes/cases/dense-prediction-vs-classification-architecture.md](notes/cases/dense-prediction-vs-classification-architecture.md) - 用 dilated convolutions 说明 dense prediction 如何逼出不同于 classification 的架构判断。更新：2026-04-11
- [notes/cases/vision-architecture-branching-points.md](notes/cases/vision-architecture-branching-points.md) - 将当前视觉材料拆成“深层可训练性”和“dense prediction 结构”两条问题线。更新：2026-04-11

## Outputs

- [../outputs/rnn-lstm-phase-summary-2026-04-08.md](../outputs/rnn-lstm-phase-summary-2026-04-08.md) - 基于三份 RNN/LSTM 资料形成的阶段总结。更新：2026-04-08
- [../outputs/rnn-next-research-directions-2026-04-08.md](../outputs/rnn-next-research-directions-2026-04-08.md) - RNN/LSTM 主题下一阶段应补的研究方向与资料计划。更新：2026-04-08
- [../outputs/rnn-transformer-research-decision-memo-2026-04-09.md](../outputs/rnn-transformer-research-decision-memo-2026-04-09.md) - 基于当前 RNN 到 Transformer 主题线形成的下一阶段研究决策 memo。更新：2026-04-09
- [../outputs/rnn-epistemology-2026-04-10.md](../outputs/rnn-epistemology-2026-04-10.md) - 围绕 Karpathy 的 RNN 文章回答“RNN 代表了作者什么样的认识论”。更新：2026-04-10
- [../outputs/knowledge-base-agent-skills-test-report-2026-04-10.md](../outputs/knowledge-base-agent-skills-test-report-2026-04-10.md) - 第一版知识库 agent skills 的静态校验与 dry run 测试报告。更新：2026-04-10
- [../outputs/llm-agents-and-harness-engineering-2026-04-10.md](../outputs/llm-agents-and-harness-engineering-2026-04-10.md) - 讲解如何利用 LLM 的特性开发 agents，以及 harness 工程的关键边界与常见坑。更新：2026-04-10
- [../outputs/agent-harness-minimum-architecture-2026-04-10.md](../outputs/agent-harness-minimum-architecture-2026-04-10.md) - 将 agent harness 拆成最小闭环组件、状态层和评估层的工程蓝图。更新：2026-04-10
- [../outputs/highway-networks-vs-resnet-2026-04-10.md](../outputs/highway-networks-vs-resnet-2026-04-10.md) - 比较 Highway Networks 与 ResNet 在解决深层网络优化问题时的不同工程哲学。更新：2026-04-10
- [../outputs/dense-prediction-vs-classification-architecture-2026-04-11.md](../outputs/dense-prediction-vs-classification-architecture-2026-04-11.md) - 解释 dense prediction 为什么会逼出不同于 classification 的架构取舍。更新：2026-04-11
- [../outputs/vision-architecture-next-research-directions-2026-04-11.md](../outputs/vision-architecture-next-research-directions-2026-04-11.md) - 当前视觉架构分支的下一步补资料顺序与缺口判断。更新：2026-04-11
