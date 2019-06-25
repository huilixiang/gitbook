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
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;$$= \underbrace{\large \int_zlnP(x,z)Q(z)dz - \int_zQ(z)Q(z)dz}_{L(Q) - Evidence lower bound} \underbrace{ - \int_zln\frac{P(z|x)}{Q(z)}Q(z)dz }_{KL}$$


