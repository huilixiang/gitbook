# 线性模型
## 大纲
- [线性模型](#linear_model)
- [回归与分类](#rgr_cls)
- [正则化与先验](#rgl_pri)
- [逻辑回归的损失函数](#lr_loss)
- [广义线性模型](#glm)

## 线性模型<span id="linear_model"></span>
响应变量(因变量)y是关于预测变量（自变量）x的线性函数
### 简单线性模型
只有一个预测变量
$$ y_i = w_0 + w_1x_i + \epsilon_i $$
### 多元线性模型
具有多个预测变量
$$ y_i = w_0 + w_1x_{1i}+w_2x_{2i}+...+w_nx_{ni} + \epsilon_i  $$   
### 回归与分类<span id="rgr_cls"></span>
y是定量变量-->回归， 常用线性回归
y是定性变量-->分类， 常用逻辑回归
### 线性回归
- 预测变量是定量变量
- 误差项独立且服从$$N(0, \sigma^2)$$
- 预测变量X与响应变量Y的真实关系F是未知， 用一个线性函数G去近似F
- 衡量G与F的近似程度    
  RSS: $$ \sum_{1}^{n} \{y_{i} - G(x_{i})\}^{2} $$
- 求解过程， 找到合适的G，使得RSS最小, 最小二乘  
### 分类问题
- 对于二分类问题可以直接用线性回归？
- 如果要预测属于某个类别的概率呢？
- 多分类怎么办？
### 逻辑回归
- logit函数  
 ####  $$ ln(\frac{p}{1-p}) = w_0 + w^TX $$
- logit反函数 logistic function:
 ###  $$ p(X) = \frac{e^{w_0 + w^TX }}{1+e^{w_0 + w^TX} }$$
- 极大似然  
  给定X,W时，$$ Y \subseteq{\{0,1\}} $$  
      
  $$ p(Y|X,W) \sim Bernoulli(\varphi) $$
  
  假设所有的Y独立同分布， 则联合概率密度：
  #### L(w) = $$\prod_{i}^{n} p(x)^y \cdot (1-p(x))^{1 - y}$$
  #### max L(w) 
  
### 正则化与先验 <span id="rgl_pri"></span>

- 似然函数联想到先验和后验
- 极大后验  
  $$ p(W|Y,X) \propto f(Y|X,W)p(W|X) = f(Y|X,W)p(W) $$
- ridge: $$p(W) \sim N(0, \lambda^2) $$ 
- lasso: $$p(W) \sim Laplace(0, \lambda) $$

### 逻辑回归的损失函数 <span id="lr_loss"></span>
- 熵 , 系统的混乱程度或者不纯度。 p：表示随机变量的概率分布函数，$$p_{i}$$代表随机变量i发生的概率
  #### $$H(y) = \sum_{i}p_{i}log\frac{1}{p_{i}} = -\sum_{i}p_{i}logp_{i}$$
- 交叉熵  y的真实分布一般未知， 我们只有近似分布 $$\hat{p}$$. 此时系统混乱程度
  #### cross entropy $$ = -\sum_{i}p_{i}log\hat{p}_{i}$$ 
- 当 $$ i \sim Bernoulli(p) $$ 时， 极大似然的负对数与cross entropy 损失一致

### 广义线性模型<span id="glm"></span>
- 响应变量服从期望为u的指数分布
- u一般是$$ \beta^{T}x的非线性函数 $$， 故有些人称其为非线性模型。但GLIM的提出者认为其是线性的，因为预测变量只能通过线性组合来影响Y的分布
- 

- y与x之间的非线性关系
  $$ g(y) = \varphi(X) + \epsilon  $$ 



  
  
