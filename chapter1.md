# 机器学习的目标函数和评价指标

机器学习的首要问题是选择目标函数，然后采用不同的算法对特征进行模型训练。获得好的结果再部署到实际中去应用。

本章主要研究机器学习中的主要目标函数，为了防止目标函数过拟合，采取的惩罚措施。以及在分类、回归、信息检索中常见的模型评价指标，这些模型评价指标通常反应一个模型的好坏程度。

* 目标函数：不仅要考虑模型的预测值和真实值的差别，还要考虑模型复杂度、过拟合等问题。一般追求score最大、loss最小。
* 损失函数

log-loss log损失函数：$$ L(y,p)=-log(y,p)= -y*log(p)+(1-y)*log(1-p)$$

MSE 平方损失函数：

0-1损失函数：

1. 惩罚项
2. 模型评价

GitBook allows you to organize your book into chapters, each chapter is stored in a separate file like this one.

