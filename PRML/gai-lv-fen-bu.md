## 概率分布
### 密度估计
在给定有限次观察的前提下，对随机变量分布p(x)建模的问题
###参数法与非参数法
- 参数法： 假定分布有一定的函数形式
- 非参数密度估计法： 分布的形式依赖于数据集的规模。通过也包含参数，但这些参数控制的是模型的复杂度而不是分布的形式。如直方图法、最近邻法以及核函数

### 二元变量

#### 伯努利分布
- 概率分布 $$B(x|u) = u^x(1-u)^{1-x} , E[x] = u, var[x] = u(1 - u)$$. 
- 有观测集D， 假设样本iid, 则关于u的似然函数为： $$p(D|u) = \prod u^x(1-u)^{1-x} $$

#### 二项分布
- N次0/1实验中， x=1的观测出现的次数M的分布称为二项分布

#### beta分布
- 二项分布的极大似然解会出现严重的过拟合，故需要引入合适的u先验。
- 先验分布是某个因子与$$u^x(1-u)^{1-x}$$的乘积，我们选择一个正比于u和(1-u)的幂指数的先验概率分布，使用后验概率分布与先验有相同的形式， 这种性质叫共轭。
- 从二项分布到正态分布推导： <br/>
  $$n! \approx \sqrt{2 \pi n } e^{-n} n^{n}  $$ <br/>
  $$C^k_n = \frac{n!}{k!(n-k)!}  \approx \frac{\sqrt{2 \pi n } e^{-n} n^{n}}{\sqrt{2 \pi k } e^{-k} k^{k} * \sqrt{2 \pi (n-k) } e^{-(n-k)} (n-k)^{n-k}} $$ <br/>
    $$ = \frac{1}{\sqrt{2\pi n\frac{k}{n} \frac{n-k}{n}}} * \frac{1}{(\frac{k}{n})^k*(\frac{n-k}{n})^{(n-k)}} $$  令 $$\hat{p} = \frac{k}{n}$$ <br/>
    $$ = \frac{1}{\sqrt{2\pi n \hat{p} (1 - \hat{p})}} * \frac{1}{\hat{p}^k * (1 - \hat{p})^{n-k}} $$
    
  $$B(n, p, k) = C^k_np^k(1-p)^{n-k} \approx \frac{1}{\sqrt{2\pi n \hat{p} (1 - \hat{p})}} * \frac{1}{\hat{p}^k * (1 - \hat{p})^{n-k}} * p^k(1-p)^{n-k} $$ <br/>
  $$ = \frac{1}{\sqrt{2\pi n \hat{p} (1 - \hat{p})}} * (\frac{p}{\hat{p}})^k * (\frac{1-p}{1-\hat{p}})^{n-k} = \frac{1}{\sqrt{2\pi n \hat{p} (1 - \hat{p})}} * exp\{kln\frac{p}{\hat{p}} + (n-k)ln\frac{1-p}{1-\hat{p}}\}$$ </br>
  $$ = \frac{1}{\sqrt{2\pi n \hat{p} (1 - \hat{p})}} * exp\{-nH(\hat{p})\}   其中H(\hat{p}) = \hat{p}ln\frac{\hat{p}}{p} + (1-p)ln\frac{1-\hat{p}}{1-p}, n \to \infty ,  p - \hat{p} = 0$$ <br/>
  对$$H(\hat{p})进行三阶泰勒展开：$$<br/>
  $$\frac{\partial H(x)}{x} = ln\frac{x}{p} - ln\frac{1-x}{1-p}$$ <br/>
  $$\frac{\partial^2 H(x)}{x^2} = \frac{1}{x} + \frac{1}{1-x}$$ <br/> 
  $$\frac{\partial^3 H(x)}{x^3} = -\frac{1}{x^2} + \frac{1}{(1-x)^2}$$ <br/> 
  $$ H(\hat{p}) = H(p) + {H}'(p)[\hat(p) - p] + \frac{1}{2}{H}''(p)[\hat{p} - p]^2 + \frac{1}{6}{H}'''(p)[\hat{p} - p]^3 $$ <br/>
  $$ = \frac{1}{2}(\frac{1}{p} + \frac{1}{q}) + O|\hat{p} -p|^3$$ <br/>
  
  所以：
  $$B(n, p, k)= \frac{1}{\sqrt{2\pi n \hat{p} (1 - \hat{p})}} * exp\{-\frac{n}{2pq}(\hat{p} - p)^2 + O|\hat{p} -p|^3\} = \frac{1}{\sqrt{2\pi n pq}} * exp\{\frac{-(k - np)^2}{2npq}\} $$ <br/>
  $$ = \frac{1}{\sqrt{2\pi \sigma}} * exp\{\frac{-(k - \mu)^2}{2\sigma^2}\} . 其中\sigma^2 = npq, \mu = np  $$
  
#### 高斯分布与顺序估计
#### 学生t分布
- 可以看成将无限多个同均值不同精度的正态分布相加， 对离群点不敏感。
#### 周期变量与极坐标
### 指数族分布
- 参数为$$\eta$$的变量x的指数族分布定义为具有下面形式的概率分布的集合： <br/>   
  $$p(x|\eta) = h(x)g(\eta)exp\{\eta^T\mu(x)\}$$
  
  
  


  