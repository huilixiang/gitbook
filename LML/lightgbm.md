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
