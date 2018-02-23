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
（9）Feature Hashing：以 user id 為例，透過一個 hash function 把每一個 user id 映射到 (hashed1_, hashed_2, ..., hashed_m) 的某個值。
（10）Category Embedding
（11）Entity/relation/path Embedding
