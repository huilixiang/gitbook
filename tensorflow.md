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
- 模型的参数一般都被保存在由variable控制的tensor中。

### 实现
#### client
- client是TFS 中主要的组件， 通过session与master、多个工作进程交互。
#### devices
- devices是TF的计算核心。
#### tensor
- 是一个有类型的、多维数组。

### node placement
- 给定一个计算图，一个主要的工作是把它映射到不同的设备上。
- 节点分配算法： cost model.
- 算法首先模拟执行计算图， 使用贪心算法然后为每个节点分配一个设备。 在真正执行的时候分配方法也如此。
- 从图的源节点开始，遍历图，对于每个节点都使用贪心算法找一个可能的节点。 筛选逻辑： 支持当前操作， 执行时间、与该节点交互消耗的时间

#### cross-device communication
- node placement被计算后， 整个图会被分成若干个小图，每个设备上一个小图。跨设备的x-->y的边会被删除，代之的是x到新的send node的边和， 一个recv的node到Y的边。 在运行期间， 由send node 和recv node来协调传输从x->y的数据。
- 这样做的好处： 减少数据传输次数、内存占用。 同时可以去中心化， 将worker与device之间的同步工作拆解开来， 由send-recv自主协调， 使得master不需要做此类工作