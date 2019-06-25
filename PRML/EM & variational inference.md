## EM 与 VI
### 推导过程
#### 贝叶斯公式
$$\large p(z|x) = \Large \frac{p(x,z)}{p(x)}$$ 
则 $$\large p(x)=\Large \frac{p(x,z)}{p(z|x)}$$
两边取对数
$$\large lnP(x) = \large lnP(x,z) - lnP(z|x)$$
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;$$\large=ln\frac{P(x,z)}{Q(z)} - ln\frac{P(z|x)}{Q(z)}$$
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;$$\large=lnP(x,z) - lnQ(z) - ln\frac{P(z|x)}{Q(z)}$$
两边取期望
$$\large \int_zlnP(x)Q(z)dz = lnP(x)$$
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;$$= \underbrace{\large \int_zlnP(x,z)Q(z)dz - \int_zlnQ(z)Q(z)dz}_{L(Q) - Evidence lower bound} \underbrace{ - \int_zln\frac{P(z|x)}{Q(z)}Q(z)dz }_{KL}$$

至此， KL >= 0 , 所以当KL=0的时候， Q分布与P一致，　但现实中我们不知道P，　所以KL=0不能利用。转而向ELOB。

#### ELOB的上界
$$lnP(x) = \large ln\int_zP(x,z)dz = ln\int_z\frac{P(x,z)}{Q(z)}Q(z)dz = ln E_{Q}[\frac{P(x,z)}{Q(z)}]$$

jensen不等式， 对于凸函数$$\phi(x)$$
$$\phi(E[x]) \leq E[\phi(x)]$$ , 凹函数相反。ln是凹函数， 故接上面公式：
$$\large \geq E_Q[ln\frac{P(x,z)}{Q(z)}] = \underbrace{E_Q[lnP(x,z)] - E_Q[lnQ(z)]}_{ELOB} $$ 

让ELOB接近其上限

#### mean-field理论 
平均场假设复杂的多变量Z可拆分为一系列相互独立的多变量Zi，i=1,⋯,M，且q分布可以因子化为这些多变量集的乘积：
$$Q(z) = \prod_i Q_i(z_i)$$  

$$\large L(Q) = \int_zlnP(x,z)Q(z)dz - \int_zlnQ(z)Q(z)dz$$
$$\large =\int \prod_i Q_i(z_i)lnP(x,z)dz - \int \prod_i Q_i(z_i) \sum lnQ_i(z_i)dz $$
$$\large = \int_{z_j}Q_j(z_j)(E_{i \ne j}[lnP(x,z)])dz_j - \int_j Q_j(z_j)lnQ_j(z_j)dz_j + const$$
令$$ln\overline{P_j}(x,z_j) = E_{i \ne j}[lnP(x,z)] $$ 
$$ = \int_{z_j} Q_j(z_j)ln\frac{\overline{P_j}(x,z_j)}{Q_j(z_j)} + const \rightarrow -KL(E_{i \ne j}[lnP(x,z)] || lnQ_j(z_j)) $$ ELOB也是一个KL， 且最大值是0.

最后介绍如何获得稳定lnQ的迭代步骤：
$$\large lnQ_1^*(z_1) = \int_{Q_2}\int_{Q_3}\cdot\cdot\cdot\int_{Q_n}lnP(x,z)Q_2(z_2)\cdot\cdot\cdot Q_n(z_n)dz_2dz_3\cdot\cdot\cdot d_zn$$




