# User-Controllable Recommendation via Counterfactual Retrospective and Prospective Explanations

## 一句话总结
这篇论文把“解释”和“控制”放到一起，认为用户只有理解推荐为何出现以及行为会造成什么后果，才谈得上真正控制系统。

## 论文做了什么
作者提出一个统一框架，让用户既能回看过去哪些行为导致了当前推荐，也能预估当前交互会如何影响未来推荐，从而通过解释来施加控制。

## 核心方法
论文分别定义了 retrospective explanation 和 prospective explanation，并基于 counterfactual reasoning 生成可操作的控制建议；同时给出 controllability complexity 和 controllability accuracy 两类评估指标。

## 结果与意义
在 MovieLens 和 Yelp 上，方法不仅能提升控制能力，还显示给用户更多控制选项有机会改善未来推荐质量，说明 controllability 不一定和 accuracy 对立。
