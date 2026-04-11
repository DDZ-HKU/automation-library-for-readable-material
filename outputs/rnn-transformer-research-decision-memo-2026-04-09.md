# RNN 到 Transformer 研究决策 Memo

日期：2026-04-09

## 结论

当前这条知识线已经足够清楚地表明：

- `RNN/LSTM` 的关键价值在于序列建模与递归状态表示
- `Bahdanau attention` 首先修补的是 `fixed-length context vector` 瓶颈
- `seq2seq-for-sets` 暴露了强行线性化与顺序敏感性的问题
- `Transformer` 的关键断点在于改变了信息访问方式，而不只是“更大更快”
- `GPipe` 说明当 Transformer 被证明有效后，瓶颈会转移到训练系统

因此，下一阶段不应继续补“RNN 还能做什么”的材料，而应进入“范式比较与瓶颈澄清”阶段。

## 当前判断

这条主题线当前最值得保留的判断有三条：

1. `RNN -> LSTM` 主要是优化与训练可行性的修补
2. `seq2seq -> Bahdanau attention` 主要是对 fixed-length bottleneck 的修补
3. `Bahdanau attention -> Transformer` 主要是把 attention 从辅助读取机制升级为主架构
4. `Transformer -> GPipe` 主要是系统扩展问题，而不是表示问题

这意味着后续阅读必须有意识地区分：

- 架构收益
- 优化收益
- 系统收益

## 当前缺口

现在最大的缺口不是“再多看一篇 Transformer 介绍”，而是下面三类空白：

### 1. 缺 RNN/LSTM 局限性的系统总结

当前已有材料能看出问题，但还没有一篇专门把：

- 长路径传播
- 状态压缩瓶颈
- 顺序计算限制

系统讲清楚的材料。

### 2. 缺 Transformer 之后的系统扩展脉络

现在只到 GPipe，还不足以形成“超大模型训练系统如何演化”的判断。

### 3. 缺 attention 到 self-attention 的中间桥梁

Bahdanau attention 已经补齐，但从 cross-attention 式对齐机制走到 Transformer 的 self-attention 主架构，中间还缺更细的演化脉络。

## 不建议继续补的方向

当前阶段先不建议优先补这些：

- 再补一篇泛泛的 “RNN/LSTM 很有效” 文章
- 继续补更多字符级生成样例材料
- 继续补只强调 benchmark 分数提升、但没有明确机制变化的模型论文

原因：

- 这些材料大概率只会重复已有认识
- 对“为什么范式切换”这个核心问题帮助有限

## 接下来最该补的 3 类材料

### 1. 一篇专门讲 RNN/LSTM 局限性的材料

目标：

- 把“为什么会换范式”讲清楚
- 不是靠回忆结论，而是靠专门分析瓶颈

为什么排第一：

- 现在 Bahdanau attention 已经补齐，最值得补的是它为什么在当时显得必要
- 否则你知道修补方案，但还不够清楚被修补的旧瓶颈到底有多本质

### 2. 一篇 attention 到 self-attention 的桥梁材料

目标：

- 看清从对齐机制到主架构的关键跃迁
- 避免把 Bahdanau attention 和 Transformer attention 直接混成同一种东西

优先补的内容类型：

- attention 变体演化
- cross-attention 与 self-attention 的区别
- 从 seq2seq 补丁到 attention-first 架构的断点

### 3. 一篇 GPipe 之后的大模型训练系统材料

目标：

- 让“系统问题”不只停留在 GPipe
- 看清 pipeline parallelism 之后，社区又如何组合 tensor/data/pipeline 方案

为什么现在就该补：

- 否则你会把“Transformer 很强”理解成纯架构问题，而忽略规模能力与系统设计之间的耦合

## 推荐阅读顺序

建议按下面顺序继续：

1. 先补 RNN/LSTM 局限性总结
2. 再补 attention 到 self-attention 的桥梁材料
3. 再补 Transformer 之后的训练系统材料

不要反过来。

原因是：

- 现在 attention 起点已补，但不先补 RNN 局限性，你就很难判断 attention 为什么会出现
- 不补 attention 到 self-attention 的桥梁，你就会把“有 attention”误解成“已经是 Transformer”
- 系统层扩展应放在架构断点基本清楚之后

## 每读完一篇后的动作

后续每篇新论文读完后，都用下面模板压缩成决策：

- 这篇论文属于架构、优化还是系统问题？
- 它真正改了什么机制？
- 它暴露了什么瓶颈？
- 它对当前主题线的影响是加强、修正，还是推翻？
- 下一篇该补什么？

## 一句话行动建议

下一步优先补 “RNN/LSTM 的瓶颈总结” 和 “attention 到 self-attention 的桥梁材料”，而不是继续补泛化的成功案例；这会直接决定你对 `RNN/LSTM -> attention -> Transformer` 这次范式转移的理解是否扎实。
