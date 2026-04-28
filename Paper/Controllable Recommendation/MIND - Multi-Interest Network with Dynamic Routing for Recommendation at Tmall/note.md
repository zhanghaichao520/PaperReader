# Multi-Interest Network with Dynamic Routing for Recommendation at Tmall

## 一句话总结
这篇论文是工业界多兴趣推荐的经典工作，核心思想是用多个兴趣向量而不是一个向量来表示用户。

## 论文做了什么
作者观察到电商用户通常同时有多个相互独立的兴趣，单一 embedding 很难兼顾，因此提出在召回阶段显式学习多个兴趣表示。

## 核心方法
MIND 通过动态路由机制把历史行为聚成多个兴趣 capsule，再用 label-aware attention 在目标物品到来时选出更相关的那部分兴趣来匹配，从而提升召回质量。

## 结果与意义
论文在 Tmall 场景中验证了多兴趣建模的工程有效性，也为后续大量多兴趣推荐方法奠定了非常直接的结构范式。
