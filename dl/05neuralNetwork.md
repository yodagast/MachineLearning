#### Keras 基本概念
- core模块，包括全连接层、激活层、Dropout层、Flatten层、Reshape层、Lambda层、ActivityRegularizer层、Masking层等

- **卷积层**（Convolutional）：![](http://i.imgur.com/KPyqPOB.gif)
- 池化（Pooling）对卷积层进行池化采样。包括maxPooling、AveragePooling等。
- **BatchNormalization** 对上一层的输出规范化，使其均值为0，方差为1。作用：（1）加速收敛 （2）控制过拟合，可以少用或不用Dropout和正则 （3）降低网络对初始化权重不敏感 （4）允许使用较大的学习率
- **Dropout层** Dropout将在训练过程中每次更新参数时按一定概率（rate）随机断开输入神经元，其他数值被随机缩放到1/(1-rate)，Dropout层用于防止过拟合。
给定一个矩阵
>\[[3., 0.5,  -0.5,  2.,7.],                  
[2., -0.4,   7.,  3., 0.2]]，

在执行Dropout后生成矩阵。
>\[[ 3.75,   0.625, -0.,     2.5,    8.75 ]
 [ 2.5,   -0.5,    8.75,   3.75,   0.   ]]

- **Embedding层** 嵌入层将正整数（下标）转换为具有固定大小的向量，如\[[4],[20]]->\[[0.25,0.1],[0.6,-0.2]]，通常用在文本分类模型中。

- **Recurrent循环层** //TODO。

#### 损失函数
度量训练中真实值和预测值之间的差值。常见的损失函数包括：mean_squared_error、mean_absolute_error、hinge、log-loss其中的计算过程包括：
Logloss:  $ L(L|P(Y|X))=-logP(Y|X)$
hinge-loss:  $L(L|P(Y|X))=max(0,1-Y*p(Y|X))$
adaboost指数损失函数：
$$f_m(x)=f_{m-1}(x)+\alpha_m G_m(x)$$
$$\arg \min_{\alpha,G}=\sum_{i=0}^{N}exp[-y_{i}(f_{m-1}(x_i)+\alpha G(x_{i}))]$$
指数损失函数的标准形式如：
$$L(y,f(x))=\exp[-yf(x)]$$
给定n个样本的损失函数为：
$$L(y|f(x))=\frac{1}{n}\sum_{i=1}^{n}\exp[-y_if(x_i)]$$

#### **优化器**
如何进行梯度下降算法学习权重特征。可以大致分为一阶梯度下降算法和二阶梯度下降算法，具体来说可以有以下几种梯度下降算法：（1）随机梯度下降算法。（2）小批量梯度下降（Mini Batch Gradient Descent）（3）动量（Momentum）（4）Nesterov梯度加速法（5）Adagrad方法（6）AdaDelta方法（7）Adam算法（Adaptive Moment Estimation）；也有基于在线学习的梯度下降学习算法如FTRL。

**一阶梯度下降算法**对于梯度下降算法（每次更新参数 ωω 时, 都使用整个训练集的数据）、小批量随机梯度下降算法（每次更新参数时, 使用 50-256个样本）和随机梯度下降算法（每次以一个样本, 而不是整个数据集来计算梯度），可以参考：http://kissg.me/2017/07/23/gradient-descent/#bgd

**基于动量的梯度下降算法**：优化相关方向的训练和弱化无关方向的振荡，来加速SGD训练。这种新方法将上个步骤中更新向量的分量 $\alpha$ 添加到当前更新向量。其他内容参考https://blog.slinuxer.com/2016/09/sgd-comparison
$$V(t)=\alpha V(t−1)+η∇(θ).J(θ)$$

不同的梯度下降优化算法可以参考：
![](/assets/relation.png)


#### 性能评估Metrics
常见的模型评估方式包括分类、回归和排序模型评价方法。最常见的模型评价方法是AUC模型评价，通过对于tpr和fpr进行积分，也包括ROC曲线等一系列相关定义。另一模型评价函数包括precision和recall曲线。而在排序算法中常见的评价指标包括AUC、MAP、NDCG和Hit@K等。



#### 神经网模型其他概念
- 神经网络的分类。依据学习的网络架构来说分为：前向式架构（Feed Forward NetWork）、回馈式架构（Recurrent Network）和强化式架构（Reinforcement Network）。依据学习策略分类包括监督式学习分类和无监督式学习分类等。
- 神经网络的基本结构包括：输入层、隐藏层和输出层。更详细来说：全连接（FullyConnected）、激活（Activation）、卷积Convolution、Pooling、SoftmaxOutput、sotfmax和log_softmax输出层。
- 常见激活函数：softmax、sigmod、tanh、relu等。注意输入数据只能进行一次的非线性变换。
- DropOut 在模型训练时随机让网络某些隐含层节点的权重不工作，不工作的那些节点可以暂时认为不是网络结构的一部分，但是它的权重得保留下来（只是暂时不更新而已），因为下次样本输入时它可能又得工作了。每个元素都有概率p被随机化为0,但为了保持矩阵的求和不变，需要调整原来的数组中每个数值到$ \frac{1}{1-p}$倍。在测试集合中，Dropout操作不改变输入形状数值。
- BatchNorm 对中间的隐藏数组进行批标准化，计算每个data所有数据的均值和标准差，然后进行标准化。除此之外，这个算子也接受两个参数：滑动平均和滑动方差。并采用下面的公式进行更新：
>moving_mean = moving_mean * momentum + data_mean * (1 - momentum)
moving_var = moving_var * momentum + data_var * (1 - momentum)

此外BatchNorm还接受两个参数进行调整。 $$ y_i=\frac{x_i-mean(x)}{\sqrt var(x)}*\gamma_i +\beta_i$$
- Pooling 池化。pool的类型包括average pooling、max pooling、sum pooling等。
- Embedding层，只能作为模型的第一层。

#### 常见的神经网络重要网络层
CNN的两种网络层：卷积层（Convolution）滑动窗口函数和池化层（Pooling）
RNN的时间网络预测
