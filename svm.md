### SVM原理简介
* SVM的目标函数

分两个方面考虑支持向量机的目标函数。
（1）两个类之间的间隔最大化即最小化$$ \frac{1}{2}w^Tw $$。
（2）考虑错误分类的代价，对于$$y_i$$为正例$$ w^Tx \gt 0$$，对于$$y_i$$为负例 $$ w^Tx\lt0 $$，我们希望$$ w^Txy_i \gt 0$$。当$$ w^Txy_i$$为负或者小于1，带来了$$1-w^Txy_i$$的损失。
综合上述，SVM的损失函数加上模型的惩罚项和正则化。目标函数变为：

$$ L=\sum_{i=0}^n {max(0,1-w^Txy_i)}+Cw^Tw$$。
其中的hinge Loss可以类比逻辑回归中的Log Loss。

* SVM的核函数

对于线性不可分的模型，可以考虑核函数技巧对数据进行转化，将低维的数据映射到高维度的空间中，转化为线性可分模型。一个核函数K(Kernel Function) 指的是 其中x，y是n维的输入值，k(x,y)=(f(x),f(y))是从n到m(m>>n)的映射，(x,y)是点乘。
 http://www.eric-kim.net/eric-kim-net/posts/1/kernel_trick.html
