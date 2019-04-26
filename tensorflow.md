## tensorflow
### 编程模型与基本概率
#### graph & nodes & edges
- 有向图。 它代表了数据流的计算， 其中一些节点负责维护&更新&持久化状态、分支与循环控制。
- 节点。 是operation的实例化。 
- 边有两种类型： 一种上面可以流动数据即tensor.  另外一种不能流数据， 只做依赖控制。

#### operation & kernels
- operation代表一个抽象的计算. 每个操作都有一个名称，如add, multiply
- kernel 是具体计算的实现。

#### sessions
- 
