## factorization machine
### abstract
- 集svm 与 因子分解模型的优势与一身
- 与svm 相比， fm用因式分解参数的方法对所有变量的相互作用进行建模。
- 适用于高维稀疏的场景（svm失败），如推荐
- 可以在线性时间内解决
- 其它因子分解模型： matrix factorization, parallel factor analysis. svd++,  它们的缺点： 不适用于通用的预估任务（prediction task）, 只适用于特征的数据、场景。并且各自的优化方法还不同。

### 介绍
- svm不适用于CF等场景。主要的原因： 在稀疏场景下，很难学到稳定的超平面。
- 另一方面，张量分解模型tensor factorization model, 不适用于prediction. 对于特殊的任务，指定的模型需要派生自己的建模和学习算法设计
- FM： 线性时间，线性个参数。优点如下：
    - 可以对非常稀疏的数据进行参数估计， 而svm在这种情况下失败
    - 线性复杂度，可以在100M的数据场景中进行预估
    - FM是一个通用的预估算法，适用于任意的实值向量， 优于其它优秀的算法：MF， SVD++, PITF, FPMC
