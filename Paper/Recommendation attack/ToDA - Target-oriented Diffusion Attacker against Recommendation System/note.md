# ToDA: Target-oriented Diffusion Attacker against Recommendation System

## 一句话总结
这篇论文把 diffusion model 引入 shilling attack，希望生成更像真实用户、同时更能精准推目标物品的攻击画像。

## 论文做了什么
作者认为传统生成式攻击在灵活性和优化稳定性上都有局限，于是探索扩散模型能否成为推荐攻击里的新一代用户画像生成器。

## 核心方法
ToDA 使用预训练自编码器把用户画像映射到潜空间，再用 Latent Diffusion Attacker 在潜空间中加噪和反推；同时借助 cross-attention 和全局二部图，把攻击目标物品信息显式注入生成过程。

## 结果与意义
实验表明 ToDA 在攻击效果和效率上都很有竞争力，这说明扩散模型不仅能做生成任务，也可能成为推荐安全领域的重要攻击工具。
