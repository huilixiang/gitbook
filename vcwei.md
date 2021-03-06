##VC 维
### 大数定理
大量随机iid的样本的均值收敛于总体均值
### 中心极限定理
在适当条件下， 大量iid样本的均值经过适当的标准化变换后依分布收敛于正态分布
### 集中不等式
一组不等式的集合， 这些不等式确定随机变量偏离总体期望的程度
#### hoeffding inequality
对于随机变量x, $$ a \leq x_i \leq b$$ 
$$P[|E[X] - \frac{1}{m} \sum_{i=0}^{m} x_{i} | > \epsilon] < 2exp(\frac{-2m\epsilon^2}{(b-a)^2})$$     

#### chebyshev`s inequality
$$P(E[f_N] - E_{N}^{*}[f_N] \geq \frac{\epsilon}{2}) \leq \frac{4var(f_N)}{N\epsilon^2}$$

### the symmetrization lemma
$$E_N 样本集， E_N^* ghost 样本集$$
$$P(sup_{f \in F}(E(f_N) - E_N(f_N)) > \epsilon) \leq 2P(sup_{f \in F}(E_N^*(f_N) - E_N(f_N)) > \epsilon/2) $$

### 问题
- LR这类简单的模型为什么应用广泛（暗含效果不错）
- bias---variance tradeoff 背后的原理或依据是什么？

### 什么是学习问题
- 术语： 大写的X/Y分别代表服从$$P_x/P_y$$分布的随机变量， 小写的x/y代表随机变量可取的具体值
- 观测样本：$$ S = \{(x_1,y_1),...,(x_i, y_i)\} $$ 
- 学习： 给定$$x_i$$ 推断 $$y_i$$    即: $$P(Y|X)$$

### 目标函数
- 联合分布 $$P(X,Y) = P(Y|X)p(X)$$, 需要知道两个分布，很难
- 直接对P(Y|X)建模--其实也挺难。 我们换个思路对：  

      两个随机变量V,W
      V = E[V|W] + (V - E[V|W])
      令Z = V - E[V|W]. 
      根据全期望公式： E[Z] = E[V] - E[E[V|W]] = E[V] - E[V] = 0!!!
      Z 与 W 无关
- 对于任意的$$(v_i, w_i)$$, 两者的关系可以描述为： 
   
  $$v_i = E[V|W=w_i] + \zeta $$ 
  其中 $$\zeta \subseteq Z$$ ，噪声项
- 我们可以把上述的关系描述应用到我们的统计模型上： 

  $$y_i = E[Y|X=x_i] + \zeta $$ . 存在一些函数： $$f(x) = E[Y|X=x] $$
 
- P(Y|X) 可以表示成如下方式：    
  $$y = f(x) + \zeta$$
  
### 假设
- 目标函数有无穷多个， 不可能穷举每个函数来找到最优的目标函数
- 一般假设目标函数f是线性、多项式甚至更复杂的非线性关系，如神经网络
- 学习的目标：找到f! 但怎样评估f对目标的拟合程度呢？ 限制条件是什么？

### 损失函数
- 假设函数 h(x)
- 损失函数   

  $$L(Y,\hat{Y})$$
- in-sample error, empirical risk:  

  $$R_{emp}(h)=\frac{1}{m}\sum_{i}^{m}L(y_{i},h(x_{i}))$$
- 选择使得$$R_{emp}(h)最优的目标函数f$$
- 问题解决了么？

### 泛化误差
- 如果我们找到了一个记忆模型，可以完全记忆训练集，使得 $$R_{emp} = 0$$
- 记忆模型其实是个很差劲的模型： 在unseen的dataset上----泛化误差
- 泛化误差R(h)较大(区别与$$R_{emp}(h)$$)
     
  $$R(h)=E_{(x,y) \sim P(X,Y)}[L(y,h(x))]$$
  如果知道了联合分布： P(X,Y)  ...想多了
  
### 联合分布很难求，学习问题还有解决方法嘛？
- $$R_{emp}(h)$$最小化时存在泛化问题
- $$R(h)$$不知道联合分布
- 换个思路：能不能让$$R_{emp}(h)$$ 近似等于 $$R(h)$$? 即： 

  $$P[\underset{h}{sup} |R(h) - R_{emp}(h)| > \epsilon]$$
  如果 $$R(h) - R_{emp}(h)$$ 的绝对值大于一个非常小的常量$$\epsilon$$的概率的上确界存在，那学习问题还有可能解决
  
### 卖个关子， 说说iid
- 现实世界很复杂，我们必须通过假设来简化理论到实际的应用
- 没有假设本身是糟糕的， 只有糟糕的假设是糟糕的
- 同分布假设： 被用来做推断的数据集是来自同一分布的， 否则最终的统计量会有很大的噪声且不能正常反应真实的分布
- 独立性假设： 数据集中的每个样本是独立的， 否则： 样本的选取有依赖，则样本集会偏向整体分布的某个方向，因此最终的统计量也不能反应真实分布

### 大数定理
- 弱大数定理： 当样本集足够大时， 样本均值趋近于总体均值   
   
  $$\lim_{m \to \infty}P[|E[X] - \frac{1}{m}\sum{x_i}| > \epsilon] = 0$$ 
- R(h) -- 总体均值， $$R_{emp}(h)$$ 是样本均值，那泛化误差的上确界概率：  

  $$\lim_{m \to \infty}P[|R(h) - R_{emp}(h)| > \epsilon] = 0$$
  看到曙光了， 还能做的更好！
  
### Hoeffding`s inequality
- LLN 指明了前进方向， 但没有告诉我们怎样可以快速到达
- 集中不等式： concentration inequalities:    

  $$\lim_{m \to \infty}P[|E[X] - \frac{1}{m}\sum{x_i}| > \epsilon] \leq 2exp(\frac{-2m\epsilon^2}{(b-a)^2})$$ 
  $$ a \leq x_i \leq b $$ , 对于二分类问题， $$(b-a)^2 == 1$$
  $$P[|R(h) - R_{emp}(h)| > \epsilon] \leq 2exp(-2m\epsilon^2)$$
- 现在针对的是单个假设函数h, 但是学习问题开始的时候并不知道是哪个h, 我们怎样利于泛化界从整个假设空间来挑选合适的假设函数呢？

### 泛化界
- 对于整个假设空间， 我们有：  

  $$P[\underset{h \sim H}{sup}|R(h) - R_{emp}(h)| > \epsilon] \leq \sum_{{h}\sim{H}} P[|R(h) - R_{emp}(h)| > \epsilon] $$ 
$$P[\underset{h \sim H}{sup}|R(h) - R_{emp}(h)| > \epsilon] \leq  2|H|exp(-2m\epsilon^2) $$
  with confidence $$1 - \delta$$
  $$|R(h) - R_{emp}(h)| \leq \epsilon \Rightarrow R(h) \leq R_{emp}(h) + \epsilon $$ 
  $$R(h) \leq R_{emp}(h) + \sqrt{\frac{ln|H|+ln{\frac{2}{\delta}}}{2m}}$$ -- 第一个泛化界公式
  泛化界与假设空间大小、数据集大小相关。 假设空间越复杂， 泛化误差的上界越大！ 
  因此记忆模型的效果不佳可以解释为： 其泛化误差的上界趋于正无穷
- 但是存在问题： 线性假设空间 H = ax + b, 但其假设空间的size |H| 趋于正无穷。 难道线性模型泛化误差上界与记忆模型一致？这与常识不符： 线性模型，感知机、svm应用广泛！ 这说明我们的理论露掉了某些东西！

### 假设空间
- 假设空间中的假设函数条件独立的假设正确嘛？
  很显然不是，以线性空间为例， 很多线性函数是线性相关的
- 
  
  



      
      
    

