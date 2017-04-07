# 逻辑回归和随机梯度下降算法

**梯度**：一元函数梯度即为导数。多元函数，梯度是一个向量，是函数在各个方向上的偏导数，是一个向量。梯度的方向是函数值变化最快的方向，梯度的大小描述当前变化的快慢。表达式（1）描述了一个三位坐标下的梯度。

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/c86221324a9d066ca28310ee772941748a5f370f "\nabla \varphi =\begin{pmatrix}
{\frac{\partial \varphi}{\partial x}},  
{\frac{\partial \varphi}{\partial y}}, 
{\frac{\partial \varphi}{\partial z}}
\end{pmatrix}")（1）

梯度下降：随机权重weights，确定学习步长 \alpha，并计算函数的梯度，反复更新更新权重。其中J\(\)

![](/assets/import_weights.png) \(2\)

