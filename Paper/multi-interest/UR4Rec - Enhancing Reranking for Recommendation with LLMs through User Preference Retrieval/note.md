# Enhancing Reranking for Recommendation with LLMs through User Preference Retrieval

## 一句话总结
这篇论文认为 LLM 做推荐重排时，问题不只是知识不足，更是喂给它的用户偏好信息太冗余。

## 论文做了什么
作者指出现有 LLM 推荐容易从长行为序列里生成一堆无关或重复的偏好描述，于是提出先检索出与当前候选最相关的那部分用户偏好，再交给 LLM 做 reranking。

## 核心方法
UR4Rec 设计了一个小型 Transformer 用户偏好检索器，围绕候选物品挑出最关键的偏好信息，相当于在用户历史和 LLM 之间搭了一层 preference retrieval bridge。

## 结果与意义
这样做既减少了提示里的噪声，也让 LLM 的重排理由更聚焦，说明“给 LLM 什么上下文”往往和“用哪个 LLM”同样重要。
