# Prompt-Based Multi-Interest Learning Method for Sequential Recommendation

## 一句话总结
这篇论文把 prompt 思想引入多兴趣序列推荐，希望不同模块看到的同一段行为序列能更贴合各自目标。

## 论文做了什么
作者指出现有多兴趣方法通常直接把历史行为同时喂给兴趣抽取器和兴趣聚合器，却忽略了这两个模块的学习目标并不一样；同时只看“中心”而忽略了行为分散度。

## 核心方法
PoMRec 为 extractor 和 aggregator 分别加入可学习 prompt，使输入更适配各自任务；此外同时利用用户交互的均值和方差表示兴趣，把 centrality 和 dispersion 一起纳入多兴趣建模。

## 结果与意义
在多个公开数据集上的结果优于已有多兴趣方法，说明 prompt 不只适用于大模型，也能作为序列推荐结构设计的一部分。
