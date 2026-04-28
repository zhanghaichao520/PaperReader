# DLCRec: A Novel Approach for Managing Diversity in LLM-Based Recommender Systems

## 一句话总结
这篇论文关注 LLM 推荐里常见的“越推荐越像”的问题，目标是在 LLM 场景下做更细粒度的多样性控制。

## 论文做了什么
作者指出现有 controllable recommendation 往往只靠单一提示词调节 diversity，这种做法太粗糙，难以表达真实用户对多样性程度和方向的复杂需求。

## 核心方法
论文提出 DLCRec，通过更细粒度的控制信号来管理 LLM 推荐过程中的多样性，让模型在相关性和多样性之间做更可解释、更可调的平衡，而不是只靠一句 prompt 粗暴约束。

## 结果与意义
实验说明 DLCRec 能更稳定地按用户意图调节多样性，价值在于它把 LLM 推荐中的 diversity control 从“提示工程”推进到了更像系统设计的问题。
