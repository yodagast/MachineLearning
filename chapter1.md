# 机器学习的目标函数和评价指标

机器学习的首要问题是选择目标函数，然后采用不同的算法对特征进行模型训练。获得好的结果再部署到实际中去应用。

本章主要研究机器学习中的主要目标函数，为了防止目标函数过拟合，采取的惩罚措施。以及在分类、回归、信息检索中常见的模型评价指标，这些模型评价指标通常反应一个模型的好坏程度。

* **目标函数**：不仅要考虑模型的预测值和真实值的差别，还要考虑模型复杂度、过拟合等问题。一般追求score最大、loss最小。通常目标函数不仅要考虑经验风险，还要考虑结构风险。

* **损失函数和打分函数：**损失函数是用来量化模型预测值和真实值差距的方式，越小越好，打分函数反之。通常在分类模型（二分类和多分类模型）、回归模型、ranking模型、聚类模型等问题。介绍一些简单的损失函数和得分函数

log-loss log损失函数

MSE 平方损失函数

0-1损失函数

ROC-score函数：

f1-score函数：F1 = 2 \* \(precision \* recall\) / \(precision + recall

r2-score函数：

* **惩罚项：**逻辑回归中$$L_1 / L_2$$ 惩罚项；XGBoost方法中的树的树数量进行惩罚。

* **模型评价**

本章节模型评价指标参考：sklearn metrics[^1]、Spark metics[^2]

[http://scikit-learn.org/stable/modules/classes.html\#module-sklearn.metrics](http://scikit-learn.org/stable/modules/classes.html#module-sklearn.metrics)

[http://spark.apache.org/docs/latest/mllib-evaluation-metrics.html](http://spark.apache.org/docs/latest/mllib-evaluation-metrics.html)

