##将要学习的内容
- 在每次只学习一层的情况下，怎么从无label数据中学习多层生成模型   

    怎样在每个隐层中添加markov随机场  
- 怎样使用生成模型进行判断训练，使得效果比分类和回归要好  

    Gaussian Processes
- 怎样在大数据集上进行非线性降维
    
- 怎样在高维序列数据上学习多层生成模型

## 机器学习任务系列

| 经典统计学       |  AI            |
|-----------------|-------------------|
| 低维 维度 < 100  | 高维 |
| 数据中有大量的噪声| 噪声不足以影响数据的内在结构（当我们使用恰当的处理方法时）|
| 数据的内在结构不复杂，用一个相对简单的模型就可以表示它| 数据有复杂的结构，不可能用一个简单的模型来表示它 |
| 主要任务是区分噪声 | 主要是任务是找到一个可学习的、能够表征数据复杂结构的方式|

## 时代背景
### 第一代nn ( ~1960)
perceptrons ,感知机， 1960年以前。 使用一个手工编码特征的层，通过学习这些特征的权重来达到识别物体
- 有一个整洁的学习方法来调整权重
- 这种学习方法从根本上限制了感知机

### 第二代nn (~1980)
#### BP算法问世
#### 小插曲
vapnik和他的同事们发明了一个聪明的感知机：SVM
- 不再使用手工编码、没有适应能力特征的层。每个训练样本会通过一定的方法生成新的特征
- 灵巧的优化方法来选择最优特征集。当在对测试样本进行分类时调整特征的权重。 本质上还是感知机。有同样的局限性
1990s,很多研究学者抛弃了多隐层的nn, 转投svm的怀抱： svm更优秀

#### BP问题在哪里
- 需要标签数据
- 训练时间太慢
- 会陷入局部最优

#### 克服BP的局限
- 保留通过梯度来调整特征权重的方法， 但拿它来对sensory input建模   

    调整生成模型的权重，使得当前sensory input的概率最大
    学习P(image) not P(label|image)
- 选择哪种类型的生成模型呢？

#### Belief Nets
- 由随机变量构成的有向无环图  
- 开始关注其中的一些变量， 可以解决两个问题： 
   - 推断问题。 推断没有关注的变量的状态
   - 学习问题。 调整变量之间的交互关系， 使得网络更倾向生成观测变量
   
- 我们使用stochastic binary variables构建的层 和 层之间加权的连接来构建网络。稍后我们会推广到其它类型的变量

#### stochastic binary units (伯努利变量)
- 只有0 / 1 状态
- 该单元被激活的概率由其它输入单元的权重决定（可以有bias）

#### 学习DBN
- 可以很容易在叶子节点产生一个无偏样本， 这样我们就可以知道网络信任哪种数据
- 所有可能隐含原因的配置的后验概率是很难推断的
- 得到一个后验样本都是极困难的
- 那我们如何来学习具有数以百万计参数的DBN?

#### sigmoid belief nets的学习规则
- 在给定观察数据的前提下， 如果我们能够从隐含状态的后验分布得到一个无偏样本 ，那么学习将会非常容易
- 可以从被抽样的父节点的二元状态  For each unit, maximize the log probability that its 
binary state in the sample from the posterior would be generated by the sampled
binary states of its parents
对于每个单元， 最大化它的状态Log概率。 单元的状态从后验分布中抽样获取。 后验分布由其它父节点的抽样状态决定。

#### Explaining away
explaining away指的是这样一种情况：对于一个多因一果的问题，假设各种“因”之间都是相互独立的，如果已经确定了是因为其中一种原因导致了结果，那么因为其他原因导致了该结果的概率就会下降。
- 即使两个条件独立的隐节点， 他们也可以变成有依赖的。 当我们观察到一个会同时影响他们的现象。 
    当我们知道有地震发生时， 房子因卡车而跳起来的概率就减小了
    

####  为什么每次学习sigmoid belief nets的一层是困难的
- 学习权重W ，需要知道第一个隐层的后验分布
- 问题1： 由于explaining away, 后验概率是极其复杂的
- 问题2： 后验概率依赖先验和似然概率
- 问题3： 为了得到第一隐层的先验我们就得整合所有更高隐层的所有可能配置

#### 两种类型的生成nn
- 使用有向无环图连接随机二元神经元的sigmoid belief net
- 使用均衡连接连接随机二元神经元的Boltzmann Machine

#### 受限bolztmann machine
- 通过限制连通性简化训练
    - 单隐层
    - 隐层节点之前没有连接
- 在RBM中， 在给定可见节点时， 隐层节点之间是条件独立的
    - 当给定一个数据向量时， 我们可以很容易的从后验分布中得到一个无偏样本
    - 这是有向信念网络的巨大优势

#### The Energy of a joint configuration



#### Weights --> Energies --> Probabilities
- 每个可视节点与隐层节点之间的可能存在的连接有能量。

    能量有权重和偏置决定(Hopfield 网络)
- 能量决定概率  

  #### $$ p(v,h) \propto  e^{-E(v,h)}  $$

- 关于可视节点的配置的概率等于所有 joint configurations 的概率之和

#### 使用能量来定义概率

















