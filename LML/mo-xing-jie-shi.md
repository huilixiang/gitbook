## 模型解释
## Shapley Values
 一个样本的特征值可以看作是游戏中的 “玩家”， 而预测值则是"付出的筹码"。 来自于博弈论。
### 思路
#### 场景
- 训练了一个预估公寓价格的模型， 对于一套公寓， 它给出了30w欧的预测， 需要对这个预测做出解释， 公寓的特点： 50平， 2楼， 附近有一个公园，不能养猫。
- 该模型对所有公司的预估均价是： 31w。 问题： 相对于average prediction, 每个特征的对当前prediction的贡献是多少？
- 如果是线性模型， 就相对简单。 权重*feature_value即可。  玩家组成一个联盟，从总回报中接收一份特征的收益。  shaply value: 是一个根据玩家的贡献来分配收益的方法。
- game -- 游戏， 对应于dataset中一个instance 的prediction
- gain -- 真实预测值 - 平均预测值。
- player -- feature value
- 结合刚才的例子， feature_values: 50平， 2楼， park-nearby, cat-banned.
- gain: 30w - 31w = -1w. 这也是我们要解释的原因。

#### 如何计算一个特征值的Shapley value
- Shapley value = average marginal contribution of a feature value across all possible coalitions.
- 





## Local Interpretable Model-agnostic Explanations. 
### 摘要
机器学习模型尽管被广泛应用， 但仍然被当作一个黑箱来看待。“信任”一个模型， 是基于一个模型的预估做出决策的基础。
LIME， 通过学习一个局部的可解释的模型， 可以实现对任意分类给出可解释的、值得依赖的解释。

### 简介
- 如果用户不相应模型或者它的预测， 那么就不会使用它。
- 区别两个两者的不同是相当重要的：
    1. trusting a prediction.   decision making. 
    2. trusting a model .  模型会在可用验证集上有一个准确度的评估。然后， real-world data往往有很大的不同。 甚至， 评估指标不能反应产品的目标。 因此，关注个体的预测值和相应的解释， 就变得相当重要 。 在大数据集上， 引导用户关注哪些instances, 也是相当重要。

- LIME。 一个可解释所有分类型或回归模型的局部近似算法
- SP-LIME。  可筛选一批具有代表性的解释实例， 来表明模型的可信任性。
- 

### the case for explanations
- data leakage. 向训练集泄漏了某些信息。比如病人Id
- data shift. 训练集与测试集差异较大

### desired characteristics for explainers.
- intepretable.  变量与输出之间的定性理解。 需要根据受众有所不同。 与输入的特征维数有区别
- local fidelity. 在被预测的实例的小范围内， 必须与模型有高于的一致性。
- model-agnostic.  模型无关
- global perspecitve

### LIME
fidelity - interpretability trade-off   
要解释的模型： $$f: R^d \rightarrow R， f(x) $$是预测值。 
解释模型: $$g \in G ， G$$是所有可能的解释模型集合
解释模型复杂度: $$\Omega(g)$$
局部

 