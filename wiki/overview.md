# Overview

这个知识库用于围绕一个或多个长期主题做持续研究。

当前状态：

- 仓库结构已初始化
- 代理维护规则已建立
- 已 ingest 多批真实资料与知识地图型材料
- `outputs/` 已预留用于保存报告、答案和分析
- `wiki/notes/` 已开始承担“默会知识层”，并细分为 workflows / frameworks / cases

当前已进入 wiki 的主题：

- 熵与复杂性的区别
- Aaronson 提出的 `complextropy`
- 以资源约束的 sophistication 刻画中间态复杂性
- RNN/LSTM 的序列建模直觉
- LSTM 如何通过 cell state 与门控缓解长程依赖
- LSTM 训练时 dropout 应施加在哪些连接上
- Relational Memory Core 如何把 multi-head attention 引入 recurrent memory 并增强 relational reasoning
- 字符级语言模型如何学到风格、格式和局部结构
- seq2seq 为什么会对输入/输出顺序敏感
- 如何把 set 结构数据接入 seq2seq / LSTM
- Bahdanau attention 如何打破 fixed-length context bottleneck
- attention 在 pre-Transformer 时代如何先作为集合读取机制出现
- Transformer 如何把 attention 从辅助机制升级为主要架构
- 超大 Transformer 如何借助 pipeline parallelism 跨多设备训练
- ResNet 如何把深层网络的优化困难重写成 residual reformulation 问题
- Identity Mappings in Deep Residual Networks 如何把 ResNet 从成功技巧推进成更稳定的 identity / pre-activation 结构原则
- Highway Networks 如何用 gated carry/transform path 打开极深前馈网络的可训练性
- Dilated Convolutions 如何为 dense prediction 扩张感受野而不损失分辨率
- AlexNet 如何把大数据、GPU、ReLU 与 dropout 组装成视觉深度学习的规模化突破
- Variational Lossy Autoencoder 如何把 VAE 的 latent code 重定义为对高层结构的 lossy 表征，而把低层细节交给 autoregressive decoder
- ToolLLM 如何把真实 API 数据、检索、规划和评估系统化为开源 LLM 的 tool-use 能力链
- LATM 如何把 tool making 与 functional cache 引入 LLM 长时服务与工具复用结构
- CREATOR 如何把抽象工具创建与具体决策执行解耦
- ToolLibGen 如何把离散工具重构成结构化工具库，缓解 tool retrieval scaling 问题
- LLM 如何进入 API synthesis / program synthesis 旁支，而不只是 agent-style tool governance
- AI/AGI 也可以被组织为一张跨 29 学科、6 学科簇的知识地图，而不只是按单一模型路线叙述
- 控制论可以作为理解 RL、RLHF、agent feedback loop 与 harness 的统一中层语言
- 复杂性科学可以作为理解 scaling、涌现能力、多主体系统与 agent ecology 的整体行为语言
- 博弈论与经济学可以分别从互动结构、偏好与激励两层补齐 agent / alignment 线
- agent harness engineering 已从最小闭环框架扩展到 coding-agent 外层 harness、长时运行 harness 与工业级 orchestration 案例
- harness 主题线已开始分化出 `guides vs sensors` 和 `trace-driven harness optimization` 两个更细粒度框架
- harness 主题线已开始补齐长时运行问题，尤其是 `context reset / compaction / handoff` 的区分
- harness 主题线已开始补齐工业案例层，尤其是 Stripe Minions 对 deterministic infrastructure 的强调

当前工作模式：

- 人负责选择资料、提出问题、判断重点
- LLM 负责摘要、整合、交叉引用、输出沉淀与巡检
- 对 PDF 资料，先经 `marker` 转成 Markdown，再进入 `raw/ -> wiki/` 流程
- 对需要更高层理解的问题，LLM 还负责把显性知识提升为可复用的默会知识解读
- 默会知识层已开始沉淀通用判断模板，而不仅是单主题解读
- 默会知识层已开始沉淀论文阅读模板，用于识别机制、瓶颈与迁移价值
- 默会知识层已开始形成从论文阅读到研究决策的完整导航链
- 默会知识层已开始沉淀“读完论文后下一步做什么”的决策模板
- `RNN/LSTM -> attention -> Transformer` 的中间桥梁已经开始补齐
- tool 论文分支已开始反向塑造知识库自身设计，形成 `atomic -> facade -> planning -> governance` 的工具治理视角

建议起步范围：

- 先选一个具体主题
- 先 ingest 3 到 5 份资料
- 在第一次真实使用后再微调 `AGENTS.md`
