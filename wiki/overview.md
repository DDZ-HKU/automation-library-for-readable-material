# Overview

这个知识库用于围绕一个或多个长期主题做持续研究。

当前状态：

- 仓库结构已初始化
- 代理维护规则已建立
- 已 ingest 14 份真实资料
- `outputs/` 已预留用于保存报告、答案和分析
- `wiki/notes/` 已开始承担“默会知识层”，并细分为 workflows / frameworks / cases

当前已进入 wiki 的主题：

- 熵与复杂性的区别
- Aaronson 提出的 `complextropy`
- 以资源约束的 sophistication 刻画中间态复杂性
- RNN/LSTM 的序列建模直觉
- LSTM 如何通过 cell state 与门控缓解长程依赖
- LSTM 训练时 dropout 应施加在哪些连接上
- 字符级语言模型如何学到风格、格式和局部结构
- seq2seq 为什么会对输入/输出顺序敏感
- 如何把 set 结构数据接入 seq2seq / LSTM
- Bahdanau attention 如何打破 fixed-length context bottleneck
- attention 在 pre-Transformer 时代如何先作为集合读取机制出现
- Transformer 如何把 attention 从辅助机制升级为主要架构
- 超大 Transformer 如何借助 pipeline parallelism 跨多设备训练
- ResNet 如何把深层网络的优化困难重写成 residual reformulation 问题
- Highway Networks 如何用 gated carry/transform path 打开极深前馈网络的可训练性
- Dilated Convolutions 如何为 dense prediction 扩张感受野而不损失分辨率
- AlexNet 如何把大数据、GPU、ReLU 与 dropout 组装成视觉深度学习的规模化突破

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

建议起步范围：

- 先选一个具体主题
- 先 ingest 3 到 5 份资料
- 在第一次真实使用后再微调 `AGENTS.md`
