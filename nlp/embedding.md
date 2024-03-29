### 图的表示学习算法

#### wod2vec
介绍word2vec原理，包括 n-gram 和skip-gram等

**(1)基本介绍**

Word2Vec是一种基本的词向量表示，通过降维将一个高维度的词向量变为低维度的向量表示。Word2Vec可以用来进行聚类、同义词分析、作为其他神经网络模型的输入层等。如果把词作为一个K维度的特征，那么就可以寻找句子、文章的更深层次特征表示。

**(2)词向量表示**

* one-hot 词向量表示。对于某个预料库中的词，可以表示为$[0,0,…,1,…,0]$的形式其中的1表示第i个单词在预料库中出现过。
* TF-IDF 词向量表示。对预料库中的词，第i个词可以被替换成这个词在文档中出现的TF\*IDF值，这和one-hot 的词向量模型相似。
* 除了基本的TF-IDF，LSA和LDA模型也是常见文本向量模型。
* Word2Vec 词嵌入。对于one-hot的词表示方法进行降维，将n维度的词向量转化为k维度的词向量进行知识表示（word represetation）。下面介绍如何学习低维度的词向量模型。

**(3)N-gram**

* CBOW。在自然语言的句子中，如“中国 的 首都 是 北京”预测第3个词语“北京”，可以结合语句的上下文进行预测。

$$ p(w_t|context)=p(w_t|w_{(t-k)}...w_{(t-1)},w_{(t+1)}...w_{(t+k)})$$

* Skip-Gram。和CBOW相反，Skip-Gram在模型预测中，基于第t个词预测第t+j个词。skip-gram通过最大化所有文档的 average log probability来进行模型预测。skip-gram采用$p(w_{t+j}|w_t)$来预测t+j个位置上的单词。对$ p(w_{t+j}|w_t) $采用softmax模型。

对于这两个模型的详细解释可以参照原paper进行阅读理解。下图有一个直观的解释。

![](/assets/import_CBOW.png)

**(4)Hierarchical Softmax**

这种层次的softmax算法结合了霍夫曼树编码。每个词w都可以沿着根节点的一条路径L找到。记:
$$n(w,1)=root,....,n(w,L(w))=w$$从root到w包含的标签分为0和1，如“01001”表示w的路径。这样在进行预测时候，我们希望在根节点第一次，softmax计算得到的概率尽量为0,第二层尽量为1,依次类推得到全部五层的概率。对这五层的概率进行似然估计，计算概率最大化的过程类似逻辑回归。在预测过程中，通过hierarchical softmax可以得到每个叶子节点的权重，即可作为每个词的词向量。

Hierarchical Softmax通过二叉树进行分类，使一连串的二分类用来进行多分类计算。过程类似于：是否是名词-&gt;是否是物品-&gt;是否是水果-&gt;是否是橘子。

除了Hierarchical Softmax进行模型的预测。作者还如何进行负采样（negative sampling）、如何降低频繁词的概率等方法。详情参考作者的论文和代码。
参考资料：http://www.cnblogs.com/wei-li/p/Word2Vec.html

#### DeepWalk
- DeepWalk 思路类似word2vec，使用图中节点与节点之间的共现关系学习节点的向量表示，将随机游走的路径节点作为当前节点的向量表示。
- DeepWalk包括两个步骤：（1）随机游走采样节点序列，（2）使用skip-gram学习向量表示，采用hierarchy softmax进行超大规模分类的分类器。

#### node2vec
node2vec是一种综合考虑DFS邻域和BFS邻域的graph embedding方法。按照一定的概率算法来进行有偏的随机游走算法。

#### LINE
- 定义图中的一阶相似度（直接相连节点的相似度）和二阶相似度（通过公共节点相连的相似度）。

- **一阶相似度**：形式化描述为若$u$, $v$之间存在直连边，则边权$w_{uv}$即为两个顶点的相似度，若不存在直连边，则1阶相似度为0。
- **二阶相似度**：对于每个顶点维护两个embedding向量，一个是该顶点本身的表示向量，一个是该点作为其他顶点的上下文顶点时的表示向量。对于有向边 $(i,j)$ ，定义给定顶点 $v_i$ 条件下，产生上下文(邻居)顶点 $v_j$ 的概率为
$$p_2(v_j|v_i)=\frac{exp(c_ju_i)}{\sum_{k=0}^{N}exp(c_ku_i)}$$


#### GNN
GNN是将图的邻居节点聚合，并计算得到图中节点的向量。
$$h_v^k=\sigma(w_k \sum_{u\in N(b)\cup v} \frac{h_u^{k-1}}{\sqrt{|N(u)||N(v)|}})$$
其中$w_k$是节点$v$在第$k$层的向量表示；$\sigma$是聚合函数，如ReLU。
- GCN：GCN是谱图卷积的一阶局部近似，是一个多层的图卷积神经网络，每一个卷积层仅处理一阶邻域信息，通过叠加若干卷积层可以实现多阶邻域的信息传递。
- GraphSage 对GNN进行改进，$AGG$可以选择Mean、Pool、LSTM等不同的聚合函数对参数进行学习。
$$h_v^k=\sigma(w_kAGG（\{h_u^{k-1},\forall u \in N(v)\} ）$$
- Graph Attention采用attention的方法学习权重，参数$\alpha_{v,u}$可以用不同的方法定义attention。
$$h_v^k=\sigma(\sum_{u\in N(b)\cup v}\alpha_{v,u}w^kh_u^{k-1}）$$

GraphEmbedding参考资料：https://github.com/shenweichen/GraphEmbedding
GraphNeuralNetwork参考资料：https://github.com/shenweichen/GraphNeuralNetwork
