## BERT

### 1. Embedding词向量
- word embedding: 无预训练
- type embedding： 前一句$E_A$，后一句$E_B$
- position embedding： 为attention增加时序信息

### 2. Transformer Encoder语言模型
- multi-head attention
  - expand（类似bagging/boosting）
  - layer norm:行样本norm（batch norm对列样本norm）
  - residual
  - Feedforward
- self attention：可并行计算
  $$ attention(q,k,v)= softmax(\frac{Q^TK}{\sqrt {d_k}})V$$
  - $\sqrt{d_k}$ 保持训练过程中梯度稳定
  - $Q^TK$ 加权求和

![](/assets/bert.jpg)


### 3. Loss
-  NextSentence Prediction
- Mask LM Loss
最多15%的词被mask， 其中80%的词被随机替换成为[Mask]，10%的词保持不变，10%的词随机替换为其他词。

### 4. pretrain & fine-tuning


### 5. 下游任务
- single text
  - GLUE
- text pair
  - SQuAD
  - SWAG

![](/assets/BERT_1.PNG)
参考资料：
https://zhuanlan.zhihu.com/p/50913043
