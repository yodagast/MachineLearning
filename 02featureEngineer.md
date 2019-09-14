### Hidden Technical Debt
**复杂模型** （1）模型的特征变化影响模型预测结果，导致模型不稳定，难以分析模型，可以将特征进行拆分，构建预测模型；（2）业务发生变化，预测模型的优化需要进行调整改进。（3）模型反馈问题，模型梯度下降，训练数据选择都是随机的，需要考虑使用随机数保证模型稳定。有时候，页面上两个相关模型也会互相影响，这种模型反馈很难看出。
**数据依赖**（1）不稳定的数据，如TFIDF计算，lookup table等，需要对数据进行备份保存（2）特征互相影响，特征不断变化，冗余特征等。需要对特征进行leave-one-out实验或专家知识。
**系统问题** 机器学习系统需要构建

**参数问题** 机器学习需要很多可配置的参数，包括（1）特征选择（2）数据选择（3）算法参数（4）数据的特征工程（5）模型评估方法等。
**Other Debt**机器学习包括很多其他领域的问题，（1）机器学习模型很难再现；（2）一个公司需要保存上百个机器学习模型，如何管理不同的机器学习模型也是重要的挑战；（3）文化的挑战，一个公司的机器学习需要研究和工程实践，团队文化决定了一个公司的机器学习模型方法。


### 大规模机器学习特征工程

**缺失值补全**
   dense-matrix ：（1）drop 有缺失值的rows；（2）numberical数据：均值、中位数、0或-999等进行补全。（3）categorical 数据：众数、改为others类别
   sparse-matrix 默认缺失值为0，通常采用如libsvm的数据格式进行数据编码。

**Feature Engineer**
（1）标准化x-mean/stdv；
 (2)归一化将数据缩放到[0,1]或者[-1,1]之间；
（3）Rounding，将浮点数值转化为分类特征；
（4）log特征转化
（5）Binarization 特征进行0-1二值化；
（6）分桶如将年龄转化为[小孩、青年、中年、老人]等。
（7）One-hot Encoding：如果某個特徵有 m 个值（例如 Taipei, Beijing, Tokyo），那它 one-hot encode 之後就成为长度为 m 的向量
（8）Count Vectorization：给定一个Array("a", "b", "b", "c", "a")计算获得这个Array的Count Vector (3,[0,1,2],[2.0,2.0,1.0])
（9）Feature Hashing：以 user id 為例，透過一個 hash function 把每一個 user id 映射到 (hashed1_, hashed_2, ..., hashed_m) 的某個值，容易出现特征冲突。Locality Sensitive Hashing包含一系列hash算法：（1）Bucketed Random Projection for  Euclidean Distance；（2）MinHash for Jaccard Distance
（10）Category Embedding
（11）Entity/relation/path Embedding

**其他特征工程**
（1）Tokenizer
（2）StopWordsRemover
（3）n-gram
（4）Polynomial Expansion
（5）StringToIndexer/IndexToString
（6）TF-IDF
（7）Word2Vec