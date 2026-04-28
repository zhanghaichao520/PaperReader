# Edit Less, Achieve More: Dynamic Sparse Neuron Masking for Lifelong Knowledge Editing in LLMs

## 一句话总结
这篇论文的核心观点是：连续知识编辑不该粗粒度改整层参数，而应该尽量只改真正承载目标知识的少数神经元。

## 论文做了什么
作者针对 lifelong knowledge editing 里常见的误差累积和能力退化问题，提出一种更细粒度的神经元级编辑框架，希望在持续编辑时尽量少伤及无关能力。

## 核心方法
NMKE 先做 neuron-level attribution，把知识相关神经元区分为 general 和 specific 两类，再结合熵引导的动态稀疏 mask，只修改和目标知识强相关的神经元。

## 结果与意义
在大量顺序编辑实验中，NMKE 在编辑成功率和通用能力保持上都优于已有方法，说明“少改但改准”是长期编辑场景里更稳的路线。
