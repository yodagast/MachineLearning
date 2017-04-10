# 贝叶斯算法及其拓展

### 朴素贝叶斯算法假设

特征之间相互独立。如果特征之间不相互独立，采用贝叶斯网络等算法。

### 朴素贝叶斯公式

$$ p(y|x1,...,xn)=\frac{p(y)*p(x_1,...x_n|y)}{p(x_1,...x_n)} $$\(1\)

$$ p(xi|y)=\frac{p(y,x_1,...x_{i-1},x_{i+1},...x_n)}{p(y)} $$\(2\)

$$ p(y|x1,...,xn)=p(y)\prod{p(x_i|y)} $$\(3\)

$$y=argmaxp(y)\prod{p(x_i|y)} $$\(4\)



（1）式是基本的朴素贝叶斯公式；（2）式利用先验概率计算了p\(x\|y\)；从而得到（3）p\(y\)正比于p\(y\)乘以p\(x\|y\)；（4）式对所有可能的类别计算概率，最终分类为概率最大的类。
