---
layout: post
title:  An obscure reason of GPU memory leak in pytorch
description: A short debug note on why I kept getting CUDA out of memory error in my codes. Main takeaway is, don't use in-place operations in your computing graph unless necessary. If you are applying it to non-leaf tensors, change it even it seems necessary. I tested on both 1.13 and 2.0, with cuda version 11.6 and 11.7.
tag: tech
comments: true
---
Recently I am transfering some of my prvious tensorflow and jax codes into pytorch. About the comparison between the three frameworks, we could have another 10 blogs to argue, but that is not what I want to share today. 

During the testing of my torch codes, I noticed the allcated cuda memory kept increasing as the training loop went. And apparently I didn't make any obvious mistakes like appending my loss term to the log before itemizing it. 

So driven by my curiosity and perfectionism, I decided to debug my codes line by line, and finally find this largely unnoticed issue: 

If `x` is a non-leaf tensor, e.g. `x` is the output of a linear layer, in-place operations like 

```python
x /= torch.norm(x, dim=-1, keepdim=True)
```
 
will cause the memory leak issue and keep increasing the memory every time you call this line. And changing it to 
 
```python
x = x / torch.norm(x, dim=-1, keepdim=True)
```

will totally solve the issue. 

The above issue is super easy to reproduce in both `1.13` and `2.0`, as shown in the following picture:

<center>
<figure>
<img src='https://raw.githubusercontent.com/minhuanli/imagehost/master/img/20230508232046.png' alt='Figure1' width='100%'/>
</figure>
</center>

So, the takeaway is: avoid in-place operations in your pytorch computing graph.
