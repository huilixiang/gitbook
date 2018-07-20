### LightGBM: a highly effecient gradient boosting decision tree

#### abstract
- 现有的GBDT实现在高维、大数据集上时性能不能令人满意，主要原因在于： 对于每个特征，需要扫描所有样本计算增益来决定分裂点。 这是耗时的关键
- Gradient-based One-Side Sampling (GOSS)
- Exclusive Feature Bundling  (EFB)