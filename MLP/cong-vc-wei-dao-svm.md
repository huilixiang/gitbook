### 背景
包调的多了，困惑也更多了。
1. 机器学习是如何与统计学基在一起的？
2. 简单如斯的LR模型为何横行天下？
3. 为什么要有训练集和测试集？ 理论依赖是什么？

### 机器学习的公式化定义
#### 问题定义
- 观测样本：$$ S = \{(x_1,y_1),...,(x_i, y_i)\} $$ 
- 学习： 给定$$x_i$$ 推断 $$y_i$$    即: $$P(Y|X)$$

#### 目标函数的由来
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

  $$y_i = E[Y|X=x_i] + \zeta $$ . 存在一些函数： $$h(x) = E[Y|X=x] $$
 
- P(Y|X) 可以表示成如下方式：    
  $$y = h(x) + \zeta$$
  
### 如何学习
#### 问题
- 如何评价目标函数学习的拟合程度？  

#### 经验风险最小？（in-sample error, empirical risk）
- $$R_{emp}(h)=\frac{1}{m}\sum_{i}^{m}L(y_{i},h(x_{i}))$$

#### 泛化误差
- 如果我们找到了一个记忆模型，可以完全记忆训练集，使得 $$R_{emp} = 0$$
- 记忆模型其实是个很差劲的模型： 在unseen的dataset上表现不符合预期
- 泛化误差R(h)较大(区别与$$R_{emp}(h)$$)
     
  $$R(h)=E_{(x,y) \sim P(X,Y)}[L(y,h(x))]$$
  如果知道了联合分布： P(X,Y)  ...想多了
  
#### 联合分布很难求，学习问题还有解决方法嘛？
- $$R_{emp}(h)$$最小化时存在泛化问题
- $$R(h)$$不知道联合分布
- 换个思路：能不能让$$R_{emp}(h)$$ 近似等于 $$R(h)$$? 即： 

  $$P[\underset{h}{sup} |R(h) - R_{emp}(h)| > \epsilon]$$
  如果概率较小， 那表明泛化间隙较小的可能性较大。 问题有可能被解决。

#### 大数定理
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












