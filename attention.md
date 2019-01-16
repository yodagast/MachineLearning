## Attention is All you Need

(1)一个基于Keras实现的Dense Attention

inputs = Input(shape=(input_dims,))
attention_probs = Dense(input_dims, activation='softmax', name='attention_probs')(inputs)
attention_mul = merge([inputs, attention_probs], output_shape=input_dims, name='attention_mul', mode='mul')


(2)Attention机制的基本思想是，打破了传统编码器-解码器结构在编解码时都依赖于内部一个固定长度向量的限制。如图是Google Transformer的一个模型框架。

![Attention](/assets/Attention.PNG)