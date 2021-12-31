---
layout: post
title: Attention I, Jointly Learn to Align and Translate  
tags: AI&Physics Attention
katex: True
progress: 5%
comments: true
---

We are witnessing the popularity and fast development of the Attention Mechanism in the deep learning community in recent years. It serves as the pivotal parts in most state-of-the-art models in NLP tasks, and continues to be a rapid evolving research topics in CV field. Besides, in recent AI-related scientific breakthroughs, like AlphaFold 2, the Attention Mechanism looks like an omnipresent component in the models. That is why we (Kevin and I) decided to start a journal club to read and discuss seminal papers about how attention was introduced and further developed. We hope this discussion could bring us more intuition about this fancy name, such that we could apply it to problems we are interested in with more confidence. 

This blog is a note of the first discussion, about the paper [*Bahdanau, et al. (2014) Neural machine translation by jointly learning to align and translate*](https://arxiv.org/abs/1409.0473). As an early (or first) implementation of "Attention Mechanism" in the translation task, it helps a lot, at least for me, to understand what is attention, although the attention here is a little different from that in the following Transformer model. <!--more--> 

1. list
{:toc}

### <i class='contrast'>Translation Task and Seq2Seq Model</i>

There are two major approaches in machine translation tasks: Traditional phrase-based translation system consists of many small sub-components that are tuned separately; Neural machine translation aims at building a single neural network that can be jointly tuned to maximize the translation performance. 

Seq2Seq Model[^1] belongs to a family of encoder-decoders in the neural machine translation approach. They typically encode a source sentence into a **fixed-length** vector, from which a decoder generates a translation. 

<i class='contrast'>Seq2Seq: RNN Encoder-Decoder</i>

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
h_{t}=f\left(x_{t}, h_{t-1}\right) \\
\tag{2}
$$


### <i class='contrast'>References</i>

[^1]: Sutskever, Ilya, Oriol Vinyals, and Quoc V. Le. "Sequence to sequence learning with neural networks." Advances in neural information processing systems. 2014.



