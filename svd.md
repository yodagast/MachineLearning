### SVD基本原理
- **PCA算法**

首先考虑特征值和特征向量。$Ax=\alpha x$其中A是一个$n×n$的矩阵，x是一个n维度的向量。如果我们求出了A矩阵的n个特征值$$\alpha_1 \lt ……\lt \alpha_i \lt …… \lt \alpha_n$$，那么矩阵A就可以表示为$ A=W\sum W$其中$\sum$是这n个特征值组成对角元素的$n×n$的矩阵。一般我们保证$||W_i||=1$。此时$W$的n个特征向量为标准正交基,$W$为对应特征值的特征向量。

- **SVD算法**

当A不为方阵时，如A是一个$m×n$的矩阵我们定义A的SVD为
$$A=U \sum V^T$$其中U是一个$m×m$的矩阵，V是一个$n×n$的矩阵，且都为单位矩阵。
计算方法:将$A^T×A$作为一个$n×n$的矩阵，进行特征分解得到
$$(A^T×A)u_i=\lambda_i u_i$$同理$A×A^T$作为一个$m×m$的矩阵，进行特征分解得到$$(A×A^T)v_i=\lambda_i v_i$$

- **CUR分解算法**

SVD算法计算比较耗时，存储$U,R$比较占用空间。CUR分解是另外一个选择，其目标是：找到输入矩阵的一个“尽可能好”的分解为三个矩阵的乘积A = CUR，SVD分解是完美的分解（通过允许误差来加速计算）。其中：
  - CC矩阵由AA矩阵中的列构成
  - RR矩阵由AA矩阵中的行构成
  - UU矩阵由C,RC,R的交集进行伪逆求得

 **Matrix Factorization**

MF将user-item组成的稀疏矩阵进行降维度处理，学习user和item的embedding表示。Spark中[ALS](http://spark.apache.org/docs/latest/mllib-collaborative-filtering.html)被用来解决MF问题，能高性能切有效的并行化计算。对于一个user和一个item之间评分的计算可以采用userVector点乘itemVector进行计算；如对于item推荐，可以选择最相似的topK个商品即可。对于MF矩阵分解的模型的评价，可以采用MAP、AP@K等。

**Factorization Machine**
传统的线性回归模型并未考虑特征之间的交互，即：
$$y(x)=w_0+w_1y_1+...+w_ny_n=w_0+\sum{} w_ix_i(1)$$
(1)式种仅仅考虑$x_i$和$x_j(i!=j)$是单独孤立的情况，并没有考虑特征分量之间的相关关系。改写为：
$$y(x)=w_0+\sum_{i=0}^{n} w_ix_i+\sum_{i=0}^{n-1}\sum_{j=i+1}^{n}w_{ij}x_ix_j(2)$$
（2）式对观察样本中未出现过交互的特征分量，不能对相应的参数进行估计。进一步改写为：
$$y(x)=w_0+\sum_{i=0}^{n} w_ix_i+\sum_{i=0}^{n-1}\sum_{j=i+1}^{n}（v_{i}^Tv_j）x_ix_j(3)$$
(3)式中$\hat{w}=v_{i}^Tv_j$对应一种对于矩阵分解，因此将（3）式中的方法称作张量分解机（Factorization Machine）模型，其中的核心在于学习$\hat{w}$，可以采用随机梯度下降、最小二乘法、马尔科夫链蒙特卡洛法等方法进行参数预估。
参考资料:
FM：https://www.cnblogs.com/pinard/p/6370127.html
PCA & SVD: http://www.cnblogs.com/leftnoteasy/archive/2011/01/19/svd-and-applications.html
CUR: http://www.ryanzhang.info/data-mining/cur-dimension-reduction-cur%E5%88%86%E8%A7%A3-%E9%99%8D%E7%BB%B4/
