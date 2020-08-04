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
###### GOSS 推导
- 通过分裂后的方案来代表增益
- O表示在一个特定的决策树节点上的数据集大小。 特征j在值d片分裂的增益，由下式代表：  

    $$ V_{j|O}(d) = \frac{1}{n_{O}} (\frac{(\sum_{x_{i} \in O:x_{i,j} \leq d} g_{i})^2}{n^{j}_{l|O}(d)} + \frac{(\sum_{x_{i} \in O:x_{i,j} \gt d} g_{i})^2}{n^{j}_{r|O}(d)}) $$
    
    where $$n_{O} = \sum I[x_{i} \in O], n^{j}_{l|O}(d) = \sum I[x_{i} \in O:x_{ij} \leq d] $$

###### EFB 算法推导
- 图着色问题 把特征看作是顶点， 如果两个特征不是互斥的，那么它们之间添加一条边。 很少有特征是完全的互斥的，所以我们
    1. 构建加权图， 边的权重就是两个节点的冲突度
    2. 按节点的度降序排列顶点
    3. 检查有序列表，看它是否存属于某个bundle or  需要重新创建一个bundle
- 当特征数量超过百万维时，上述方法也存在问题。提出了一个不需要构建图的近似算法
    1. 按nonzero value个数排序。 
    2.  




## LightGBM源码分析
### 执行流程  
- application.h --> Run()--> InitTrain() --> Train()
    - InitTrain  
        - init-network
        - creat boosting:  GBDT \ DART \ GOSS \ RF
        - creat objective function: regression(L2, L1), quantile, huber, binary, poisson, lambdarank..
        - LoadData： 
              - predict_fun: boosting.get()
              - 加载数据
              - 添加training_metric 
        - objective_fun.init()以binarylogloss为例：
            -  做is_unbalance处理。  正样本量 > 负样本量， 则增加负样本权重：label_weight_[0] = 正样本数 / 负样本数。 否则：增加  正样本权重
        -
    - Train     
     
### init阶段
- network init
- boost.reset
- objective_fun_reset
- load_data
- objective_fun_init
- boosting init
- boosting addValidData

### boosting
 
### objective
- GetGradients. 根据score, 计算gradients & hessians

#### BinaryLogloss
##### 构造函数
- sigmoid_ 参数， sigmod function 的参数。 仅使用于binary, multiclassova, lambdarank
- is_unbalance,  仅适用于binary & multiclassova, 如何训练集是unbalanced, 可以使用此参数。 可以提升模型的整体效果， 但可能导致较差的单个样本估计。 与参数： scale_pos_weight不能同时使用。
- scale_pos_weight. 正样本标签的权重。与is_unbalance类似
- is_pos_ : 是否是正样本。 默认 >0 即为正样本。

##### init(MetaData, num_data)
- MetaData 存储训练数据的元数据（非特征）。 例如： labels、 weights、initial scores(model will boost from, otherwise 0)、query level informations(for lambdarank).
- lebel_
- weights_
- 正、负样本个数
- 如果是分布式环境，会同步计算正负样本总合
- 如果只有正样本 or 负样本， 则不需要训练
- 默认：正样本1, 负样本-1
- 如果is_unbalance == True,   如果正样本数量 > 负样本数量 则 正样本标签的权重=1, 负样本标签的权重= 正样本数量/负样本数量。 负责相反。
- scale_pos_weight 

##### ConvertOutput
- return 1.0f / (1.0f + std::exp(-sigmoid_ * input[0])). 默认sigmoid_ = 1.0

##### GetGradients(const double* score, score_t* gradients, score_t* hessians)
- if(weights_ == nullptr): #pragma omp parallel for schedule .  
        - 遍历每一个data
        - 计算: is_pos, label(先判断is_pos, 然后从label_val_中取出对应的标识-1 or 1), label_weight.
        - 计算response: -label * sigmoid_ / (1.0f + std::exp(label * sigmoid_ * score[i]))
        - 计算abs_response = fabs(response)
        - gradients: response * label_weight  
        - hessians: (abs_response * (sigmoid_ - abs_response) * label_weight )
- else
        - gradients: response * label_weight  * weights_[i]
        - hessians: (abs_response * (sigmoid_ - abs_response) * label_weight * weights_[i])


##### BoostFromScore(int)
- suml = sum(is_pos_[label_[i]] * weights_[i])  #q
- sumw = sum(weights_[i])
- 


### treelearner
#### serial_tree_learner.cpp
- init
    - num_data_ 数据集大小
    - num_features_ 特征数量
    - max_case_size. 如果config.histogram_pool_size <=0 则为num_leaves, 否则 total_histogram_size = sum(所有特征对应的bin数量  * sizeof(HistogramBinEntry)）。 max_cache_size = config.histogram_pool_size * 1024 * 1024 / total_histogram_size

- train
    - force split的逻辑： forcedsplits_filename 可以指定每棵树首先使用的分裂特征以及分裂点， 在best_first learning之前。
    - BeforeFineBestSplit
    - ConstructHistograms 如何构建直方图。
    
