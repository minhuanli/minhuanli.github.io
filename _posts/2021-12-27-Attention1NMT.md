---
layout: post
title: Attention I, Jointly Learn to Align and Translate  
tags: AI&Physics Attention
katex: True
progress: 50%
comments: true
---

We are witnessing the popularity and fast development of the Attention Mechanism in the deep learning community in recent years. It serves as the pivotal parts in most state-of-the-art models in NLP tasks, and continues to be a rapid evolving research topics in CV field. Besides, in recent AI-related scientific breakthroughs, like AlphaFold 2, the Attention Mechanism looks like an omnipresent component in the models. That is why we (Kevin and I) decided to start a journal club to read and discuss seminal papers about how attention was introduced and further developed. We hope this discussion could bring us more intuition about this fancy name, such that we could apply it to problems we are interested in with more confidence. 

This blog is a note of the first discussion, about the paper [*Bahdanau, et al. (2014) Neural machine translation by jointly learning to align and translate*](https://arxiv.org/abs/1409.0473). As an early (or first) implementation of "Attention Mechanism" in the translation task, it helps a lot, at least for me, to understand what is attention, although the attention here is a little different from that in the following Transformer model. <!--more--> 

1. list
{:toc}

### <i class='contrast'>Translation Task and Seq2Seq Model</i>

People are trying to translate natural languages with machines. There are two major approaches in machine translation tasks: Traditional phrase-based translation system consists of many small sub-components that are tuned separately; Neural machine translation aims at building a single neural network that can be jointly tuned to maximize the translation performance. 

Before the publication of this attention mechanism paper, Seq2Seq model[^1] achieved the best results in neural translation tasks. And in fact, the attention mechanism is only a tiny but profound modification to the Seq2Seq model. So we will first review the Seq2Seq Model's architecture and limitations, then the introduction of the "attention" would be intuitive.

Seq2Seq Model belongs to a family of encoder-decoders in the neural machine translation approach. They typically encode a source sentence into a fixed-length vector, from which a decoder generates a translation. 

#### <i class='contrast'>RNN Encoder</i>

Say we have the source sentence $$\mathbf{x}$$ and the output sentence $$\mathbf{y}$$:

$$
\mathbf{x}=\left(x_{1}, \ldots, x_{T_{x}}\right), x_{i} \in \mathbb{R}^{K_{x}} \\
\mathbf{y}=\left(y_{1}, \ldots, y_{T_{y}}\right), y_{i} \in \mathbb{R}^{K_{y}} \tag{1}
$$

<p class='bluebox'>
Each natural language sentence will first be tokenized (usually includes an ending signal), and each word or token into fixed length vectors. But apparently, different sentences could have different lengths \(T_x\) and \(T_y\)
</p>

The encoder reads input sequence $$\mathbf{x}=\left(x_{1}, \ldots, x_{T_{x}}\right), x_{i}$$, and pass through a RNN (Recurrent Neural Network) like:

$$
h_{t}= \begin{cases}f\left(x_{t}, h_{t-1}\right) & , \text { if } t>0 \\ 0 & , \text { if } t=0\end{cases} \tag{2}
$$

where $$h_t \in \mathbb{R}^n$$ is a hidden state at time $$t$$ and $$f$$ are non linear functions. This iterative path will output a series of hidden states:

$$
H=\left(h_{1}, \cdots, h_{T_{x}}\right), h_{i} \in \mathbb{R}^{n}
$$

Generally, a **context vector** $$c$$ will be generated from the hidden states with another nonlinear function $$q$$, as shown in figure 1[^2]:

$$
c= q(\{h_1,\dots,h_{T_x}\})\tag{3}
$$

Usually they use the LSTM as the $$f$$, and $$c= q(\{h_1,\dots,h_{T_x}\})=h_T$$. 

<p class='redbox'>
It is intuitive to choose \(c=h_T\) at the moment, as \(h_T\) is the only hidden state which could possibly contain all information in the source sentence. But this is not a perfect choice of course, as we all know now RNN would concentrate more on the information around the node..
</p>

<center>
<figure>
<img src='https://raw.githubusercontent.com/minhuanli/imagehost/master/img/20211231000239.png' alt='Figure1' width='50%'/>
<figcaption align = 'left'><b>Fig.1 - An illustration of the RNN Encoder–Decoder in previous Seq2Seq Model, from reference 2. The choice to construct the context vector c, red circled, is the limitation of the model.</b></figcaption>
</figure>
</center>

#### <i class='contrast'>RNN Decoder</i>

The decoder is often trained to predict the next word $$y_{i}$$ given the context vector $$c$$ and previously predicted words $$\{y_1, \dots, y_{i-1}\}$$.

Again, as this is a RNN, hidden states also exist in the decoder part, generated from the previous hidden state, previous predicted word and the context vector:

$$
s_{i}=f\left(s_{i-1}, y_{i-1}, c\right) \tag{4}
$$

Then the conditional probability predict of the next word will be:

$$
p\left(y_{i} \mid y_{1}, \ldots, y_{i-1}, \mathbf{x}\right)=g\left(y_i \mid y_{i-1}, s_{i}, c\right)
\tag{5}
$$

<p class='bluebox'>
During the training process, loss function is constructed to maximize the likelihood of the true next word. Once the model is trained, they usually use algorithms like beam search that approximately maximizes the conditional probability to predict the output sentences.
</p>


#### <i class='contrast'>Problem of the Seq2Seq Model</i>

As indicated by the equation (4) and (5), a single context vector $$c$$ is used in prediction for all $$s_i$$ and $$y_i$$. That means, the RNN encoder needs to compress all the necessary information of the source sentence into a single fixed-length vector. It is not surprising that the Seq2Seq model can hardly cope with long sentences, as shown in figure 2[^3]. Fixing this issue is the motivation of the paper.

<center>
<figure>
<img src='https://raw.githubusercontent.com/minhuanli/imagehost/master/img/20220103120204.png' alt='Figure2' width='60%'/>
<figcaption align = 'left'><b>Fig.2 - The BLEU scores achieved by Seq2Seq Model. The performance decreases rapidly when the sentence length grows. From reference 3.</b></figcaption>
</figure>
</center>


### <i class='contrast'>Introduce Attention to the model</i>


### <i class='contrast'>References</i>

[^1]: Sutskever, Ilya, Oriol Vinyals, and Quoc V. Le. "Sequence to sequence learning with neural networks." Advances in neural information processing systems. 2014.

[^2]: Cho, Kyunghyun, et al. "Learning phrase representations using RNN encoder-decoder for statistical machine translation." arXiv preprint arXiv:1406.1078 (2014).

[^3]: Cho, Kyunghyun, et al. "On the properties of neural machine translation: Encoder-decoder approaches." arXiv preprint arXiv:1409.1259 (2014).

