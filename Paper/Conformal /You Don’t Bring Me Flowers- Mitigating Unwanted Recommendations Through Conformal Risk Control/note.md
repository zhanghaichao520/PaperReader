# You Don’t Bring Me Flowers: Mitigating Unwanted Recommendations Through Conformal Risk Control

## 一句话总结
这篇论文关注“用户不想看什么”，希望用有理论保证的方法把不想要的内容稳定压下去。

## 论文做了什么
作者针对个性化推荐里无关、讨厌甚至有害内容的问题，提出一个与底层推荐模型解耦的风险控制框架，只依赖简单的二元负反馈就能控制不想要内容的暴露比例。

## 核心方法
论文把 conformal risk control 引入推荐场景，对 unwanted content 的风险做可证明上界；同时结合用户的隐式消费反馈来扩展候选集合，缓解传统 conformal 方法在推荐集合过小场景下的局限。

## 结果与意义
在真实视频平台数据上的实验显示，这个方法可以以较小交互成本稳定降低 unwanted recommendations，价值在于它提供了比经验式“少推荐一点”更可靠的风险控制思路。
