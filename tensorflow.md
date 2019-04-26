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
- client通过session与TF 进行系统交互。

#### variables
- 在图中， 许多计算被执行很多次。 tensor只存活于一次计算。
- 变量是一种特殊的操作， 可以返回handle来持久化需要跨多次执行的tensor
