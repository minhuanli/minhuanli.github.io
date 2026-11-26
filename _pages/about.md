---
layout: about
title: about
permalink: /
subtitle: >
  Research Scientist &middot;
  <a href="https://biohub.org/" target="_blank">Biohub</a>

profile:
  align: right
  image: prof_pic.jpg
  image_circular: true
  # more_info: >
  #   <p>162 5th Ave</p>
  #   <p>New York, NY 10010</p>

news: true
selected_papers: true
social: true
---

I am a Research Scientist in the AI research organization at [Biohub](https://biohub.org/). Previously, I was a Flatiron Research Fellow at the [Center for Computational Mathematics](https://www.simonsfoundation.org/flatiron/center-for-computational-mathematics/), Flatiron Institute, and received my PhD in Applied Physics from Harvard, advised by [Doeke Hekstra](https://hekstralab.fas.harvard.edu/).

I am also a core member of [Reciprocal Space Station](https://rs-station.github.io/), an open-source consortium for structural biology software. During my PhD, I was a Fellow at the [Eric and Wendy Schmidt Center](https://www.ericandwendyschmidtcenter.org/) at the Broad Institute and interned at [D.E. Shaw Research](https://www.deshawresearch.com/).

My research asks how pretrained models and experimental measurements can interact in a robust, high-bandwidth way. I approach this as an interacting ecosystem of **Data** (raw measurements), **Models** (explicit parameterizations of biological state), and **Neural Priors** (pretrained foundation models), with structural biology as the main testbed:

- **Data → Model.** Differentiable forward models, better-behaved objectives in measurement space, and samplers for multimodal state spaces.
- **Prior → Model.** Pretrained models as a biologically meaningful search space, steered by experimental likelihoods at inference time.
- **Data/Model → Prior.** Raw measurements as first-class training signals, not only inference targets.
- **Prior → Data.** Using the prior's uncertainty to guide experimental design and data collection.
