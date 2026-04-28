# Enhancing Recommendation Diversity by Re-ranking with Large Language Models

## 一句话总结
这篇论文主要是在问：LLM 能不能只靠 zero-shot prompt，当一个多样性重排器来用。

## 论文做了什么
作者把 LLM 放到推荐流水线的 reranking 环节，要求它从候选列表中重排出更有多样性的结果，并系统比较不同 prompt 模板和不同 LLM 家族的表现。

## 核心方法
方法本身比较直接：给定候选排序和多样性指令，让 GPT 或 Llama 系列模型以 zero-shot 方式生成新的排序，再与随机重排和传统多样性重排方法对比。

## 结果与意义
结论比较克制：LLM 重排已经优于随机方案，但整体还不如经典 reranker 稳定；不过它展示了 LLM 未来作为通用多目标重排器的可能性。
