### LightGBM: a highly effecient gradient boosting decision tree

#### abstract
- 现有的GBDT实现在高维、大数据集上时性能不能令人满意，主要原因在于： 对于每个特征，需要扫描所有样本计算增益来决定分裂点。 这是耗时的关键
- Gradient-based One-Side Sampling (GOSS) 去除相当大比例的梯度较小的样本
- Exclusive Feature Bundling  (EFB) bundle mutually exclusive features ， 找到互斥的特征集，NP难问题，但可以用近似的贪婪算法寻找

#### introduction
##### GOSS
