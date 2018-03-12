## bayesian
### condition probability function vs likelihood function
- $$P(x|\theta)$$  . x 是变量;  积分是1。 一个事件发生的概率p <br/> 
- $$L(x|\theta)$$  . $$\theta$$是变量, 积分是任意非负值。 最有可能是哪个事件概率P发生了 <br/>

### 概率论与统计学
- 概率论： 模型的参数已知， 推测可能观测的数据是什么样的 <br/>
- 统计学： 数据已知， 模型的参数是怎样的？ <br/>

### 共轭先验
- 后验分布$$p(\theta|x)$$和先验分布$$P(x|\theta)$$ 属于相同的函数形式， 则称先验与后验是共轭分布
- 此时， 先验被称为似然函数的共轭先验

### 先验、后验、条件概率
- 随机变量x： 包含n重伯努利实验， 成功次数为s, 伯努利实验成功的概率为q-->未知
- 则x服务二项分布, 其概率质量函数为：<br/>
    $$p(s) = \binom{n}{s}q^{s}(1-q)^{n-s}$$ <br/>  
- 则先验概率q（此时q未知）的先验为贝塔分布 <br/>
    $$p(q)=\frac{q^{\alpha-1}*(1-q)^{\beta-1}}{B(\alpha, \beta)}$$
- 如果我们对x进行一次采样， 得到s次成功， f次失败， 则： <br/>
    $$p(s,f|q=x) = \binom{s+f}{s}q^{s}(1-q)^{f}$$ <br/> 
    $$p(x)=\frac{x^{\alpha-1}*(1-x)^{\beta-1}}{B(\alpha, \beta)}$$

    