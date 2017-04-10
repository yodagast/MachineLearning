# 机器学习的目标函数和评价指标

机器学习的首要问题是选择目标函数，然后采用不同的算法对特征进行模型训练。获得好的结果再部署到实际中去应用。

本章主要研究机器学习中的主要目标函数，为了防止目标函数过拟合，采取的惩罚措施。以及在分类、回归、信息检索中常见的模型评价指标，这些模型评价指标通常反应一个模型的好坏程度。

**目标函数**：不仅要考虑模型的预测值和真实值的差别，还要考虑模型复杂度、过拟合等问题。一般追求score最大、loss最小。通常目标函数不仅要考虑经验风险，还要考虑结构风险。

**损失函数和打分函数：**损失函数是用来量化模型预测值和真实值差距的方式，越小越好，打分函数反之。通常在分类模型（二分类和多分类模型）、回归模型、ranking模型、聚类模型等问题。介绍一些简单的损失函数和得分函数。

log-loss: 用于逻辑回归、softmax多分类。

hinge-loss: SVM分类器常用损失函数。

MSE : 用于线性回归损失函数计算。

0-1损失函数: 朴素贝叶斯分类。

ROC-score函数：通常只能用于二分类。

f1-score函数：F1 = 2 \* \(precision \* recall\) / \(precision + recall\)可以用于二分类和多分类。f1得分还可以分为micro，macro和weight三种打分函数。其中macro是每个类的p和r进行平均计算，micro对于每个实例做平均计算，weight不仅考虑每个类别的precision和recall得分，还考虑类的不均衡性。通常macro-f1使用较多。

F-Score 得分：$$ F =(\beta^2+1)\frac{precision * recall}{\beta^2precision + recall} $$。当$$ \beta$ =1 $$时，F-score即为F1score。

r2-score函数：

**惩罚项：**逻辑回归惩罚项l1或者l2；树方法中的树的树叶子节点数量进行惩罚。

**模型评价：**通常模型评价采用训练集和验证集进行交叉验证。常用有效的训练集合包括3-折/5-折交叉验证。依据目标函数最优，选择最合适的模型对测试集进行测试打分。

本章节模型评价指标参考：sklearn metrics[^1]、Spark metics[^2]

[http://scikit-learn.org/stable/modules/classes.html\#module-sklearn.metrics](http://scikit-learn.org/stable/modules/classes.html#module-sklearn.metrics)

[http://spark.apache.org/docs/latest/mllib-evaluation-metrics.html](http://spark.apache.org/docs/latest/mllib-evaluation-metrics.html)

