### 神经网模型初探
- 神经网络的分类。依据学习的网络架构来说分为：前向式架构（Feed Forward NetWork）、回馈式架构（Recurrent Network）和强化式架构（Reinforcement Network）。依据学习策略分类包括监督式学习分类和无监督式学习分类等。
- 神经网络的基本结构包括：输入层、隐藏层和输出层。更详细来说：全连接（FullyConnected）、激活（Activation）、卷积Convolution、Pooling、SoftmaxOutput、sotfmax和log_softmax输出曾。
- DropOut 训练过程中，每个元素都有概率p被随机化为0,但为了保持矩阵的求和不变，需要调整原来的数组中每个数值到$$ \frac{1}{1-p}$$倍。在测试集合中，Dropout操作不改变输入形状数值。

