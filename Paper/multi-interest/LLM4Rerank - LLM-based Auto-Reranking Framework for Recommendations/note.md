# LLM4Rerank: LLM-based Auto-Reranking Framework for Recommendations

## 一句话总结
这篇论文希望把准确率、多样性、公平性等多个 reranking 目标统一交给 LLM 去协调。

## 论文做了什么
作者认为现有 reranking 模型通常只能顾及少数目标，且难以根据场景变化灵活调整，因此提出一个 LLM 驱动的自动重排框架。

## 核心方法
LLM4Rerank 把 accuracy、diversity、fairness 等目标抽象成不同 aspect node，构建全连接图，让 LLM 在 Chain-of-Thought 过程中综合这些目标，并允许输入中显式调节不同目标的重要性。

## 结果与意义
实验显示该框架在多种目标上都优于已有方法，意义在于它把 reranking 从“单目标模型设计”推进到“统一语义空间中的多目标推理”。
