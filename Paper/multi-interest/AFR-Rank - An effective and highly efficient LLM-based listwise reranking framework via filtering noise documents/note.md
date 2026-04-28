# AFR-Rank: An effective and highly efficient LLM-based listwise reranking framework via filtering noise documents

## 一句话总结
这篇论文认为 LLM 做 listwise reranking 之前，先把噪声候选过滤掉，往往比直接全量重排更有效也更省钱。

## 论文做了什么
作者针对首阶段召回带来的无关文档噪声，指出这些噪声既会拖累 LLM 重排效果，也会显著抬高推理开销，因此把“先筛噪声”作为框架重点。

## 核心方法
AFR-Rank 包含 Assessor、Filter 和 Reranker 三部分：先评估候选相关性，再过滤明显无关项，最后让 LLM 在更干净的候选集上做 listwise reranking。

## 结果与意义
这种设计同时改善效果和效率，说明在 LLM reranking 场景里，候选集质量本身就是性能上限的重要决定因素。
