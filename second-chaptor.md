# 梯度下降算法

**梯度：**一元函数的梯度即为导数，多元函数的梯度是一个向量，是函数在各个方向上的偏倒数。梯度的大小表示函数在当前位置的变化快慢，梯度的方向表示当前函数值变化最快的方向。下图是一个三元函数的梯度求解算法。

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/c86221324a9d066ca28310ee772941748a5f370f "\nabla \varphi =\begin{pmatrix}
{\frac{\partial \varphi}{\partial x}},  
{\frac{\partial \varphi}{\partial y}}, 
{\frac{\partial \varphi}{\partial z}}
\end{pmatrix}")（1）

**梯度下降算法**：初始化随机权重weights，求出函数的梯度，并选择学习步长$$ \alpha $$，更新权重，直到结果收敛。

![](/assets/import_gd.png) \(2\)

**批随机梯度下降算法BGD**：每次更新m个样本的梯度，得到全局最优解。

[![](https://github.com/endymecy/spark-ml-source-analysis/raw/master/%E6%9C%80%E4%BC%98%E5%8C%96%E7%AE%97%E6%B3%95/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D/imgs/1.3.png "1.3")](https://github.com/endymecy/spark-ml-source-analysis/blob/master/%E6%9C%80%E4%BC%98%E5%8C%96%E7%AE%97%E6%B3%95/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D/imgs/1.3.png)（3）

**随机梯度下降算法SGD**：每次通过一个样本进行随机梯度迭代可能得到局部最优解。

![](http://upload-images.jianshu.io/upload_images/1825085-a08b3af9b8250e20.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)（4）

**小批量随机梯度下降算法MBGD：**每次选择b个样本如10个进行批量参数更新b&lt;&lt;m。

# 逻辑回归算法

**二分类逻辑回归：**对w\*x计算后，将值域在实数域的计算采用sigmod函数结果映射到\[0,1\]函数区间范围内。

sigmod函数 $$ f(x)= \frac{1}{1+e^-w*x} $$ 



