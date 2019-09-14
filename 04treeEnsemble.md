# 树方法和ensemble

**决策树算法**

决策树算法是树方法的基本算法。通常分为ID3、C4.5、CART算法等。核心点在于：（1）决策树的划分点选择，通常基于Gini、信息熵、信息增益率等算法进行选择。（2）决策树的切割通常采用递归切割。自顶向下进行划分。决策树停止的条件是：没有可以选择的特征进行分割、样本个数小于阈值、样本的Gini指数小于阈值或者所有数据属于同一类别即为停止。（3）决策树通常采用递归切分。每次切割基于贪婪算法使得模型的Gini系数最小。通常贪心算法不能得到全局最优。

**随机森林算法**

随机森林算法要点：（1）每个决策树输入特征输入m&lt;&lt;M，其中M是训练数据的总特征数量，通常取$\sqrt(M)$；（2）对训练数据的N个样本，进行有放回的随机抽样，并用未抽取到的样本作为预测，评估误差。（3）bagging每个决策树的权重相同，而boosting对决策树进行线性回归，可以学习每个决策树的不同权重。

**XGBoost算法**

XGBoost算法是Kaggle等实战比赛中最常用的算法之一。特点包括：（1）目标函数的**损失函数部分通过泰勒二阶展开近似**；（2）定义了树的复杂度并作为惩罚项添加到目标函数中；（3）分裂节点处通过结构打分和分割损失动态生长；（4）便于处理稀疏数据，通过行采样和列采样避免过拟合；（5）可以处理分类、回归和排序问题。

**(1)DMatrix**：DMatrix是xgboost中内置的矩阵数据结构。支持libsvm、CSR sparse Matrix或者普通的nparray矩阵。DMatrix支持设置矩阵中每一列的权重，补全缺失值等。

**(2)Booster**：booster是xgboost的学习模型，包括gblinear、gbtree和DART，linear是线性模型，而后两者是树模型。通常树模型包括参数如行采样、列采样、树的深度、个数等，DART包括设置dropout参数，GBtree还包括L1、L2惩罚项，学习步长等参数。而linear model通常需要设置L1/L2惩罚项。

**(3)Learning Objects & Metrics**：根据learning task的不同，设置不同的learning objective，选择不同的learning metrics。（1）regression，分为逻辑回归和线性回归，log-loss和rmse.\(2\)binary classification错误率、precision/recall/f1、accuracy等。\(3\) multiclass classification可以采用merror、precision/recall/f1等。（4）ranking 可以采用MAP、NDCG等指标。

**(4)其他**：（1）Xgboost提供了一个sklearn接口。（2）XGBoost提供了一个交叉验证方法。