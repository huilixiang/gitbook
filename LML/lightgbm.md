## LightGBM: a highly effecient gradient boosting decision tree

### abstract
- 现有的GBDT实现在高维、大数据集上时性能不能令人满意，主要原因在于： 对于每个特征，需要扫描所有样本计算增益来决定分裂点。 这是耗时的关键
- Gradient-based One-Side Sampling (GOSS) 去除相当大比例的梯度较小的样本
- Exclusive Feature Bundling  (EFB) bundle mutually exclusive features ， 找到互斥的特征集，NP难问题，但可以用近似的贪婪算法寻找

### introduction
#### GOSS
- 不同梯度的样本对增益的贡献是不一样的， 梯度大的样本增益贡献越大
- 在down sampling的时候， 需要保留梯度大的样本， 特别是增益的取值范围较大的时候
#### EFB
- 特征空间相当稀疏
- 特征降维的方法： 打到互斥的特征组（几乎不会同时取到非0值）
- 通过图着色的方式来实现： 把特征看作节点， 当两个特征不互斥的时候添加一条边

### Preliminaries
#### GBDT 复杂度分解
- pre-sorted algorithm 穷举法
- 基于直方图的分裂方法。 时间复杂度： 直方图构建：O(#data * #feature), 分裂点查找： O(#bin *　#feature).
- 降低复杂度的方向： 减少 #data #feature

#### 相关工作
##### 数据降维
- xgb实现了pre-sorted 和 histogram-based algorithm
- 减少#data的通用做法就是down sampling.  例如： 丢弃权重小于阈值的样本。
- 但是gbdt里面样本没有初始权重（疑问：其它的算法为什么会有呢？）
##### 特征降维
- 减少#feature. 通过pca or projection pursuit. 这些算法依赖假设： 特征集是冗余的。但这并不总是成立
- pre-sorted算法可以通过忽略0值特征的方式来降低training cost
- histogram-based算法不可以： 检索分桶值， 无论特征值是否为0。 导致GBDT不能够利用数据的稀疏性
#### Gradient-based One-Side Sampling
##### 算法描述
- adaboost, 样本权重是一个很好的数据实例重要性指标， 而GBDT没有native的样本权重，所以不能使用adaboost的采样方法
- gbdt中每个样本的梯度为样本采样提升了有用的信息
- 保留所有large梯度的样本 并且  在sample gradients中随机采样
- 根据梯度的绝对值排序， 取top a%的样本，然后从剩下的样本中随机采样b%. 然后在计算增益的时候放大sample gradients的权重，系数为： (1 - a ) / b

##### 理论分析
- 通过分裂后的方案来代表增益
- O表示在一个特定的决策树节点上的数据集大小。 特征j在值d片分裂的增益，由下式代表：  

    $$ V_{j|O}(d) = \frac{1}{n_{O}} (\frac{(\sum_{x_{i} \in O:x_{i,j} \leq d} g_{i})^2}{n^{j}_{l|O}(d)} + \frac{(\sum_{x_{i} \in O:x_{i,j} \gt d} g_{i})^2}{n^{j}_{r|O}(d)}) $$

