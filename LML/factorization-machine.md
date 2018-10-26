## factorization machine
### abstract
- 集svm 与 因子分解模型的优势与一身
- 与svm 相比， fm用因式分解参数的方法对所有变量的相互作用进行建模。
- 适用于高维稀疏的场景（svm失败），如推荐
- 可以在线性时间内解决
- 其它因子分解模型： matrix factorization, parallel factor analysis. svd++,  它们的缺点： 不适用于通用的预估任务（prediction task）。