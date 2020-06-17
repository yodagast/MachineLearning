### Attention model

#### Encoder-decoder
Encoder-Decoder框架可以这么直观地去理解：可以把它看作适合处理由一个句子（或篇章）生成另外一个句子（或篇章）的通用处理模型。对于句子对<X,Y>。 --------（思考：<X,Y>对很通用，X是一个问句，Y是答案；X是一个句子，Y是抽取的关系三元组；X是汉语句子，Y是汉语句子的英文翻译。等等），我们的目标是给定输入句子X，期待通过Encoder-Decoder框架来生成目标句子Y。X和Y可以是同一种语言，也可以是两种不同的语言。而X和Y分别由各自的单词序列构成：
$x=(x_1,x_2,……,x_m)$
$y=(y_1,y_2,……,y_n)$
其中Encoder对输入$x$进行非线性编码，转化为中间语义表示C，
Decoder根据句子$x$的中间语义表示C和之前已经生成的历史信息$(y_1,y_2,……,y_{i-1})$来生成i时刻要生成的单词$y_i$
#### Attention Model
$$Att(query,source)=\sum_{i=0}^n Similarity(query,key_i)value_i $$
- hard attention:对所有key求权重概率，每个key都有一个对应的权重，是一种全局的计算方式（也可以叫Global Attention）
- soft attention: 这种方式是直接精准定位到某个key，其余key就都不管了，相当于这个key的概率是1，其余key的概率全部是0。因此这种对齐方式要求很高，要求一步到位，如果没有正确对齐，会带来很大的影响。另一方面，因为不可导，一般需要用强化学习的方法进行训练。（或者使用gumbel softmax之类的）
- local attention: 对一个窗口区域进行计算。先用Hard方式定位到某个地方，以这个点为中心可以得到一个窗口区域，在这个小区域内用Soft方式来算Attention。
