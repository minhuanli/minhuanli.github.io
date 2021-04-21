---
layout: post
title: Temporal Difference Methods in Machine Learning
tags: BiologicalComplexity
katex: True
progress: 100%
---
This is a summary about paper *"Sutton, R.S., 1988. Learning to predict by the methods of temporal differences. Machine learning, 3(1), pp.9-44."* This paper provided a complete discussion about the temporal difference methods in the learning to predict task, which takes observations and try to predict outcomes from those observations like classification problem. This summary borrowed a lot of ideas from Tasha's presentation and centers around the comparision with the supervised learning method.<!--more-->


First is a clarification about what is temporal difference methods and what is the difference between temporal difference and supervised learning. One main difference, and also the benefit of temporal difference, is that, supervised learning can not update the prediction at each time step until the very end when it knows the actual outcome, while temporal difference can sort of update the prediction once it reaches the next step. So the temporal difference method is beneficial for the amount of computation and the storage space. Note that besides the differences we mentions above, we can show the results of temporal difference methods and supervised learning methods are generally the same with specific constuctions. 

Here are some necessary notations and formalizations. Say we have multi-step prediction problems with observation-outcome sequence $$x_{1}, x_{2}, \ldots, x_{m}, z$$ where $$x_{t}$$ is a vector of observations available at time $$t$$ and scalar $$z$$ is the outcome. The learner produces a sequence of predictions estimating $$Z$$: $$P_{1}, P_{2}, \ldots, P_{m}$$ where $$P_{t} \stackrel{\text { def }}{=} P\left(x_{t}, w\right)$$ and $$w$$ is a vector of modifiable weights. The goal of learning is to correctly update $$w$$ by determining $$\Delta w_{t},$$ an increment to $$w$$ from each observation:

$$
w \leftarrow w+\sum_{t=1}^{m} \Delta w_{t} \tag{1}
$$

Generally speaking, in supervised learning, the update will be :

$$
\Delta w_{t}=\alpha\left(z-P_{t}\right) \nabla_{w} P_{t} \tag{2}
$$

where $$\nabla_{w} P_{t}$$ is the vector of partial derivatives of $$P_{t}$$ with respect to each component of $$w$$.

And if we concentrate on a special case where $$P_t$$ is a linear function of $$x_t$$ and $$w$$ (Widrow-Hoff procedure):

$$
\Delta w_{t}=\alpha\left(z-w^{T} x_{t}\right) x_{t}
$$

Note here, for **the supervised learning method, all updates update on z**.

But the results are the same for the two methods; The key is to represent the error $$z-P_t$$ as a sum of canges in predictions:

$$
z-P_{t}=\sum_{k=t}^{m}\left(P_{k+1}-P_{k}\right) \quad \text { where } \quad P_{m+1} \stackrel{\text { def }}{=} z
$$

Using this, equations (1) and (2) can be combined as:

$$
\begin{aligned} w \leftarrow w+\sum_{t=1}^{m} \alpha\left(z-P_{t}\right) \nabla_{w} P_{t} &=w+\sum_{t=1}^{m} \alpha \sum_{k=t}^{m}\left(P_{k+1}-P_{k}\right) \nabla_{w} P_{t} \\ &=w+\sum_{k=1}^{m} \alpha \sum_{t=1}^{k}\left(P_{k+1}-P_{k}\right) \nabla_{w} P_{t} \\ &=w+\sum_{t=1}^{m} \alpha\left(P_{t+1}-P_{t}\right) \sum_{k=1}^{t} \nabla_{w} P_{k} . \end{aligned}
$$

So:

$$
\Delta w_{t}=\alpha\left(P_{t+1}-P_{t}\right) \sum_{k=1}^{t} \nabla_{w} P_{k} \tag{3}
$$

we **have an update independent of z.**  

The hallmark of temporal-difference methods is their sensitivity to changes in successive predictions rather than to overall error between predictions and the final outcome, so we modified the above equation (3) and get the following:

$$
\Delta w_{t}=\alpha\left(P_{t+1}-P_{t}\right) \sum_{k=1}^{t} \lambda^{t-k} \nabla_{w} P_{k}
$$

This is called TD$$(\lambda)$$ model. If we set $$\lambda =1$$ then the temporal diffenrce method is just the same as supervised learning.













