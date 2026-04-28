# On Practical Diversified Recommendation with Controllable Category Diversity Framework

## 一句话总结
这篇论文想解决工业推荐里的多样性问题，而且强调多样性应该是可控的，而不是固定加一点 diversity loss 就结束。

## 论文做了什么
作者把多样性拆成两种：用户显式偏好的多样性，以及用户历史里没怎么接触过类别的多样性，然后设计一个框架同时兼顾这两类目标。

## 核心方法
CCDF 分成两阶段：先做 User-Category Matching，用 DeepU2C 学出用户更可能接受的类别集合；再做 Constrained Item Matching，在这些类别里挑物品。通过可调参数控制候选类别数，从而控制最终推荐的类别多样性。

## 结果与意义
离线和在线结果都表明它尤其能提升非交互类别上的多样性，意义在于把“去过滤泡泡”从抽象目标变成了可以直接调节的工程机制。
