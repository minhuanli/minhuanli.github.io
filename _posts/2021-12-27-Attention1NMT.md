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


