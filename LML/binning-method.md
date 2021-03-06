### binning method

#### 介绍
分箱或离散化是将连续值变成类别型变量的过程。 数值型变量通常会通过基于frequency table的模型化方法来实现离散化，如决策树。此外，分箱可以通过降低噪声或非线性来提高预测精度。通过分箱还可以识别离群点、无效值、缺失值等，一般分为两大类分箱方法： 有监督和无监督的

#### 无监督  
无监督分箱方法不使用label信息，常见的有等宽和等频

##### 等宽  
将数据划分为k个区间， 
每个区间的宽度： $$w=(max - min) / k$$, 
区间的边界： min + w, min + 2w, ..., min+(k-1)w

##### 等频
将数据划分为k组， 每组内的值个数近似相同。设置k的最好的方式是通过直方图

##### 其它方法
1. rank 将数值排序，用位置来表示数值的rank, 相同的数值具有相同的rank. 缺点：rank与数据集大小相关。
2. 分位数。 缺点类似于rank
3. 数据函数： 对于高偏态分布， 使用:$$ floor(log(x)) $$ 

#### 监督方法
监督式的分箱方法会利用label信息来选择离散化的点，基于熵相关的方式都属于监督式的