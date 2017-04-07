# 逻辑回归和随机梯度下降算法

**梯度：**一元函数的梯度即为导数，多元函数的梯度是一个向量，是函数在各个方向上的偏倒数。梯度的大小表示函数在当前位置的变化快慢，梯度的方向表示当前函数值变化最快的方向。下图是一个三元函数的梯度求解算法。

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/c86221324a9d066ca28310ee772941748a5f370f "\nabla \varphi =\begin{pmatrix}
{\frac{\partial \varphi}{\partial x}},  
{\frac{\partial \varphi}{\partial y}}, 
{\frac{\partial \varphi}{\partial z}}
\end{pmatrix}")（1）

**梯度下降算法**：初始化随机权重weights，求出函数的梯度，并选择学习步长$$ \alpha $$，更新权重，直到结果收敛。

![](/assets/import_gd.png) \(2\)

