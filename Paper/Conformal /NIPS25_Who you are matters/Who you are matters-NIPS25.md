# Who You Are Matters: Bridging Topics and Social Roles via LLM-Enhanced Logical Recommendation

---

### **Project Overview**  
**Problem**:   
传统推荐系统（Recommender Systems, RS）遵循学习排序范式，主要关注物品主题（e.g., 类别）和用户基于历史互动的偏好。但忽略了用户特征和社会角色（social roles），这些是影响兴趣相关性和偏好转移的逻辑混杂因子（logical confounders）。导致模型表达力受限，无法解释如“尿布-啤酒”相关性（用户角色“新生儿爸爸”作为解释)。

**Vision**:    

![截屏2025-10-29 12.39.25](/Users/chongzhang/Library/Application Support/typora-user-images/截屏2025-10-29 12.39.25.png)

提出**TagCF** – 一个新型框架，通过整合大型语言模型（LLM）和多模态LLM（MLLM）：  
✅ 显式解决用户角色识别和行为逻辑建模任务  
✅ 提取标签并构建虚拟逻辑图，提供动态、可解释的用户行为知识  
✅ 通过模块化设计，提升推荐准确性和多样性，并证明用户角色建模优于物品主题建模，且逻辑图通用可转移  

---

###   **核心模块** 

###   ![截屏2025-10-29 12.34.26](/Users/chongzhang/Library/Application Support/typora-user-images/截屏2025-10-29 12.34.26.png)

| Module 1                                                     | Module 2                                                     | Module 3                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| MLLM-based Item-wise Tag Extraction（物品级标签提取：从多模态数据自动提取用户角色标签和物品主题标签，解决隐私和效率挑战） | LLM-based Collaborative Logic Filtering（协同逻辑过滤：基于标签推理U2I和I2U逻辑图，建模角色-主题关系） | Tag-Logic Integration in Recommendation（标签-逻辑整合：增强推荐架构、学习和推理，提升准确性和多样性） |

**Technical Pathways**:  

这几个模块的管线图：  
1. **提取阶段**：输入多模态物品信息 → MLLM（e.g., M3）生成嵌入和提示 → 提取用户标签集T和物品标签集C → 覆盖集减缩和蒸馏模型优化。  

   - 1. **特征提取：**用 MLLM 生成语义嵌入 E_i 和初始文本特征。
     2. **构建提示（prompts）：**X^T_i 用于提取用户角色标签（e.g., “从视频中推断可能的用户角色，如职业或兴趣”）；X^C_i 用于提取物品主题标签（e.g., “提取视频的主题类别，如音乐或仪器”）。提示细节在附录 B.3。
     3. **生成标签：**每个物品生成 k 个用户标签和 l 个物品标签（e.g., 视频“民乐表演” → 用户标签“民乐爱好者”、物品标签“乐器展示”）。
     4. **输出：全局标签集 T（用户标签集）和 C（物品标签集）。每天更新以覆盖新物品。**

2. **逻辑推理阶段**：输入标签集 → LLM 迭代提示推理 → 构建逻辑图G_U2I*和G_I2U* → 蒸馏模型预测连接。  

   - 1. 用 LLM 迭代推理：为每个用户标签 t 构建提示 X_t（e.g., “给定角色‘交响乐手’，适合哪些物品主题？”）→ 生成相关物品标签 C_t ~ LLM(X_t)。
   - 2. 类似，为物品标签 c 构建 X_c → 生成用户标签 T_c ~ LLM(X_c)。
   - 3. 更新标签集：T ← T ∪ T_c；C ← C ∪ C_t（迭代几次，确保覆盖）。
   - 4. 构建有向图：G_U2I*（U2I 逻辑，用户标签指向物品标签）；G_I2U*（I2U 逻辑，反向）。

   **输出：逻辑图 G*，节点是标签集 T*/C*，边是概率连接（top-b 目标标签）**。

3. **整合阶段**：标签编码器增强表示 → 对比学习对齐语义 → 推理时添加标签-逻辑分数 → 输出最终推荐（util变体偏准确，expl变体偏多样）。  

   - 1. **标签编码器（Tag-based Encoder）**：物品表示 x_i 增强为标签聚合。用户表示：两个序列模型处理 ID 和标签序列 → 合并 ϕ_u = MLP(x_u ⊕ r^{(t)}_u)。预测 ˆy_raw = Sigmoid(ϕ_u^T x_i)。

     2. **学习增强（Tag-based Learning Augmentation）**：用对比学习（CL）对齐语义。损失：ℒ_ut (用户标签匹配) + ℒ_it (物品标签匹配)，总损失 ℒ = λ(ℒ_ut + ℒ_it) + (1-λ)ℒ_ui（BCE 损失）。支持两种模式：util（原始标签，偏准确）和 expl（用逻辑图扩展标签，偏多样）。

     3. **推理扩展（Tag-logic Inference Extension）**：推理时，从 ϕ_u 推断用户标签 T_u^{(0)}，用 G* 扩展 T_u^{(1)}。计算标签匹配分 ˆy_tag = ∑ P(t|u) P(t|i)（加权 β_0/β_1）。最终 ˆy = ˆy_raw + β_0 ˆy_tag^{(0)} + β_1 ˆy_tag^{(1)}。

---

###  🌍 **系统框图**  


> 概述TagCF框架：  
> - 左侧：(1) MLLM-based Tag Extraction – 从原始信息（ASR、OCR、Text）经MLLM嵌入和提示，提取Item Tag Set和User Tag Set。  
> - 中间：(2) LLM-based Collaborative Logic Reasoning – 用提示生成U2I/I2U Logic Prompt → LLM推理逻辑图G_U2I*和G_I2U*。  
> - 右侧：(3) Tag Logic Integration – RecSys中包括Tag-based Item/User Encoder、Tag-based Learning Augmentation（对比损失ℒ= λ(ℒut + ℒit) + (1−λ)ℒui）、Tag-logic Inference Extension → 输出ˆy = ˆy_raw + ˆy_tag。  
> 整体流程：离线提取/推理 → 在线整合到推荐管道，提升性能。  

---

###  💡 **实验**  
> 实验维度：在线A/B测试（工业平台）、离线评估（工业+公共数据集）、消融研究（组件/超参敏感性）、转移测试（跨任务通用性）。方法：基线对比（e.g., SASRec, BPR），A/B分桶（8桶，每桶1/8流量），长短期测试（14-40天）。Metrics：准确性（NDCG@10/20, MRR@10/20, Interaction Rewards如play/like）；多样性（ItemCoverage@10/20, GiniIndex@10/20, Novelty-based Diversity）。  

Q1: 在线实验验证(Online A/B test›)了TagCF在工业规模下的实际提升（准确+多样），如TagCF-util提升交互0.946%，证明框架实用性。  

- **用户分配**：随机将用户分为8个桶（buckets），每个桶约占总流量的1/8，包含数千万用户，以避免偏差。

- **测试方法**：两个桶测试TagCF-util（偏向准确性）和TagCF-expl（偏向探索多样性），另两个桶使用基线模型（一个经过4年迭代的最先进排名系统）。

- **测试时长**：每种方法至少在线测试14天，确保统计可靠性。Q3: 消融和转移实验验证了每个模块的有效性和逻辑图的通用性（如工业图转移到公共数据集，提升NDCG 8-10%)。

![截屏2025-10-29 12.51.27](/Users/chongzhang/Library/Application Support/typora-user-images/截屏2025-10-29 12.51.27.png)

Q2: 离线实验验证了用户标签 vs. 物品标签的行为差异，用户标签更稳定/表达力强，提升准确性；物品标签提升多样性。 

![截屏2025-10-29 12.55.19](/Users/chongzhang/Desktop/截屏2025-10-29 12.55.19.png)

Q3: 消融和转移实验验证了每个模块的有效性和逻辑图的通用性（如工业图转移到公共数据集，提升NDCG 8-10%）。