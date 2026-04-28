# Would You Like Your Data to Be Trained? A User Controllable Recommendation Framework

## 一句话总结
这篇论文把“哪些行为可以拿去训练推荐模型”也交给用户自己控制。

## 论文做了什么
作者认为用户并不一定希望自己的全部行为都参与模型训练，因此提出一种 user-controllable recommendation 范式，让用户为不同交互指定是否愿意被用于训练的程度。

## 核心方法
方法把问题建模为多人博弈：每个用户通过 willingness vector 选择哪些样本参与训练，目标是在推荐效果和用户意愿之间求平衡。为避免每次都重训模型，论文用 influence function 近似不同选择下的推荐质量，并进一步用多 anchor 提升近似精度。

## 结果与意义
实验表明该框架能在不完全牺牲效果的前提下更尊重用户对训练数据使用的偏好，意义在于把“训练数据控制权”正式纳入推荐优化目标。
