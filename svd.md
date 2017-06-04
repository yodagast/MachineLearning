### SVD基本原理
-** PCA算法**
首先回归特征值和特征向量。$$Ax=\alpha x$$其中A是一个$$n×n$$的矩阵，x是一个n维度的向量。如果我们求出了A矩阵的n个特征值$$\alpha_1 \lt ……\lt \alpha_i \lt …… \lt \alpha_n$$，那么矩阵A就可以表示为
 $$ A=W\sum W$$其中$$\sum$$是这n个特征值组成对角元素的$$n×n$$的矩阵。
一般我们保证$$||W_i||=1$$。此时$$W$$的n个特征向量为标准正交基。

- **SVD算法**