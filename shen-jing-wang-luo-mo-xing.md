### 神经网模型初探
- 神经网络的分类。依据学习的网络架构来说分为：前向式架构（Feed Forward NetWork）、回馈式架构（Recurrent Network）和强化式架构（Reinforcement Network）。依据学习策略分类包括监督式学习分类和无监督式学习分类等。
- 神经网络的基本结构包括：输入层、隐藏层和输出层。更详细来说：全连接（FullyConnected）、激活（Activation）、卷积Convolution、Pooling、SoftmaxOutput、sotfmax和log_softmax输出层。
- 常见激活函数：softmax、sigmod、tanh、relu等。注意输入数据只能进行一次的非线性变换。
- DropOut 在模型训练时随机让网络某些隐含层节点的权重不工作，不工作的那些节点可以暂时认为不是网络结构的一部分，但是它的权重得保留下来（只是暂时不更新而已），因为下次样本输入时它可能又得工作了。每个元素都有概率p被随机化为0,但为了保持矩阵的求和不变，需要调整原来的数组中每个数值到$$ \frac{1}{1-p}$$倍。在测试集合中，Dropout操作不改变输入形状数值。
- BatchNorm 对中间的隐藏数组进行批标准化，计算每个data所有数据的均值和标准差，然后进行标准化。除此之外，这个算子也接受两个参数：滑动平均和滑动方差。并采用下面的公式进行更新：
>moving_mean = moving_mean * momentum + data_mean * (1 - momentum)
moving_var = moving_var * momentum + data_var * (1 - momentum)

此外BatchNorm还接受两个参数进行调整。 $$ y_i=\frac{x_i-mean(x)}{\sqrt var(x)}*\gamma_i +\beta_i$$
- Pooling 池化。pool的类型包括average pooling、max pooling、sum pooling等。
- Embedding层，只能作为模型的第一层。

#### 神经网络优化算法
可以大致分为一阶梯度下降算法和二阶梯度下降算法
具体来说可以有以下几种梯度下降算法：（1）随机梯度下降算法。（2）小批量梯度下降（Mini Batch Gradient Descent）（3）动量（Momentum）（4）Nesterov梯度加速法（5）Adagrad方法（6）AdaDelta方法（7）Adam算法（Adaptive Moment Estimation）
**一阶梯度下降算法**对于梯度下降算法（每次更新参数 ωω 时, 都使用整个训练集的数据）、小批量随机梯度下降算法（每次更新参数时, 使用 50-256个样本）和随机梯度下降算法（每次以一个样本, 而不是整个数据集来计算梯度），可以参考：http://kissg.me/2017/07/23/gradient-descent/#bgd
**基于动量的梯度下降算法**：
$$V(t)=\alpha V(t−1)+η∇(θ).J(θ)$$

#### CNN基本原理



