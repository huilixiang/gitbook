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

#### 如何计算一个特征值的Shaply value