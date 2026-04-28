# User-controllable Recommendation Against Filter Bubbles

## 一句话总结
这篇论文想让用户主动干预推荐列表的“同温层”程度，而不是被动等待系统慢慢学会。

## 论文做了什么
作者认为传统靠多样性或公平性目标来缓解 filter bubble 的方法往往反应慢、用户参与弱，因此提出一种允许用户直接下达控制命令的推荐原型。

## 核心方法
核心是 UCI（User-Controllable Inference）框架。它通过 counterfactual inference 估计过时用户表示对当前推荐的影响，再把用户控制信号注入推理阶段，快速修正推荐结果并缓解类别偏置。

## 结果与意义
实验表明 UCI 能在多个数据集上有效降低 filter bubble 现象，同时较好兼顾推荐质量，贡献在于把“抗过滤泡泡”从训练目标转成了可交互的推理机制。
