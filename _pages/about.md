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

I am a Research Scientist in the AI research organization at [Biohub](https://biohub.org/). Previously, I was a Flatiron Research Fellow at the [Center for Computational Mathematics](https://www.simonsfoundation.org/flatiron/center-for-computational-mathematics/), Flatiron Institute. I received my PhD in [Applied Physics](https://seas.harvard.edu/applied-physics) from Harvard University in January 2025, advised by [Doeke Hekstra](https://hekstralab.fas.harvard.edu/). I also hold a S.M. in [Computational Science & Engineering](https://seas.harvard.edu/masters-computational-science-and-engineering) from Harvard, and an undergraduate degree in Physics from [Fudan University](https://www.fudan.edu.cn/en/).

During my PhD, I was a Fellow at the [Eric and Wendy Schmidt Center](https://www.ericandwendyschmidtcenter.org/) at the Broad Institute of MIT and Harvard, and interned at [D.E. Shaw Research](https://www.deshawresearch.com/), where I worked on jointly fitting a family of QM/ML force field models to quantum mechanical and experimental data. I am also a core member of [Reciprocal Space Station](https://rs-station.github.io/), an open-source consortium for structural biology software. I care deeply about contributing to the scientific community through both computational tools and shared infrastructure.

My research asks how pretrained models and experimental measurements can interact in a robust, high-bandwidth way: models supply priors over plausible states, while measurements supply the sample-specific evidence. I approach this as an interacting ecosystem of **Data, Models, and Neural Priors**, with structural biology (X-ray crystallography and cryo-EM) as my main testbed, though many of the ideas generalize more broadly.

In this framework, **Data** are the raw measurements (e.g., cryo-EM micrographs, diffraction patterns, sequencing-based readouts); **Models** are explicit parameterizations of the biological state (e.g., atomic coordinates); and **Neural Priors** are pretrained foundation models (e.g., AlphaFold) that capture the statistical regularities of biology.

**Data → Model.** The core inverse problem: inferring the state behind a measurement. I build differentiable forward models from states to observables, objectives in measurement space with better geometry that stay well-behaved under noise and sparsity, and samplers for high-dimensional, multimodal state spaces.

**Prior → Model.** Using pretrained models as a biologically meaningful state space to search in, steered by experimental likelihoods at inference time without retraining. This makes inverse problems more efficient and scalable, and can recover information that conventional summaries compress away.

**Data/Model → Prior.** Making raw measurements first-class training signals rather than only inference targets, so foundation models learn from heterogeneous, context-rich data (sequence, structure, chemistry, evolution, and experimental readouts) instead of curated summaries alone.

**Prior → Data.** Closing the loop: using the prior's uncertainty to guide experimental design and AI-centric data collection. This is the frontier I aim to develop alongside experimental collaborators.
