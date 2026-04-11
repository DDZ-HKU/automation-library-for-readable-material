# Highway Networks vs ResNet

日期：2026-04-10

## 结论

如果只看历史位置，Highway Networks 和 ResNet 都在解决“深层网络为什么难训练”这个问题；但它们给出的答案不同：

- Highway Networks 的答案是：加可学习 gate，让信息决定“变换多少、携带多少”
- ResNet 的答案是：直接给每个 block 一条极简 identity shortcut，并把目标改写成 residual reformulation

所以两者的关键差异不是“都有 skip path”，而是：

- Highway 更像“受控信息流”
- ResNet 更像“默认直通 + 增量修正”

## Highway Networks 代表什么

Highway Networks 代表一种很强的工程直觉：

- 极深网络之所以难训练，是因为信息流和梯度流不够顺
- 所以要给每层一个 learnable gate
- 让网络自己决定什么时候该变、什么时候该过

这种思路明显受 LSTM 启发，核心是 gating。

## ResNet 代表什么

ResNet 代表另一种更激进的判断：

- 先不要让每层去决定“能不能过”
- 直接假设信息应当默认能过
- 让 block 只学习相对输入的偏移量

这使它比 Highway 更轻：

- 参数更少
- 结构更简单
- 计算负担更低
- 训练时更像一种统一默认机制，而不是层层门控

## 为什么历史最后偏向 ResNet

从当前资料看，至少有三个原因：

1. ResNet 把 skip path 思想压缩得更简单
2. identity shortcut 比 gated shortcut 更便宜
3. residual reformulation 把“学整个函数”改成“学增量修正”，叙事更强、结构更统一

也就是说，ResNet 并不是否定 Highway 的方向，而是把 Highway 中最值钱的那部分留下来，再把其余复杂性删掉。

## 一句话关系

可以把两者关系压成一句话：

Highway Networks 把“跨层直通路径”发明得更显式，ResNet 把这条路径做得更极简、便宜、可扩展。

## 研究上最值得保留的判断

这条线最值得保留的不是“谁先谁后”，而是一个更通用的判断：

- 当一个系统训练困难时，可能不需要更复杂的控制机制
- 有时更强的方法，是把困难问题改写成默认直通、只学习增量修正的问题

这也是为什么 ResNet 后来比 Highway 更像一个长期通用基元。
