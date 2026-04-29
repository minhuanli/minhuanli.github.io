---
layout: about
title: about
permalink: /
subtitle: >
  Flatiron Research Fellow &middot;
  <a href="https://www.simonsfoundation.org/flatiron/center-for-computational-mathematics/" target="_blank">Center for Computational Mathematics</a>,
  Flatiron Institute

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

I am a Flatiron Research Fellow at the [Center for Computational Mathematics](https://www.simonsfoundation.org/flatiron/center-for-computational-mathematics/), Flatiron Institute. I received my PhD in [Applied Physics](https://seas.harvard.edu/applied-physics) from Harvard University in January 2025, advised by [Doeke Hekstra](https://hekstralab.fas.harvard.edu/). I also hold a S.M. in [Computational Science & Engineering](https://seas.harvard.edu/masters-computational-science-and-engineering) from Harvard, and an undergraduate degree in Physics from [Fudan University](https://www.fudan.edu.cn/en/).

During my PhD, I was a Fellow at the [Eric and Wendy Schmidt Center](https://www.ericandwendyschmidtcenter.org/) at the Broad Institute of MIT and Harvard, and interned at [D.E. Shaw Research](https://www.deshawresearch.com/), where I worked on jointly fitting a family of QM/ML force field models to quantum mechanical and experimental data. I am also a core member of [Reciprocal Space Station](https://rs-station.github.io/), an open-source consortium for structural biology software. I care deeply about contributing to the scientific community through both computational tools and shared infrastructure.

My research builds scalable, mathematically principled methods for biomolecular dynamics. I approach this by designing an interacting ecosystem of **Data, Models, and Neural Priors**, drawing heavily on the biophysical principles underlying experiments such as X-ray crystallography and cryo-EM, generative modeling, and statistical-physics-inspired sampling.

In this framework, Data represents the raw experimental observables (e.g., cryo-EM micrographs, X-ray scattering patterns); Models are the unified parameterizations of the molecule (e.g., atomic coordinates); and Neural Priors are the foundation models (e.g., AlphaFold) that capture the statistical rules of biology.

**Data → Model.** The core inverse problem, and where I spend most of my time. I develop differentiable forward models that faithfully map molecular structures to experimental observables, robust objective functions that remain well-behaved under noise and sparsity, and efficient samplers for high-dimensional, multimodal conformational landscapes.

**Prior → Model.** Steering pretrained foundation models with experimental likelihoods at inference time — without retraining — so they serve as principled priors for the inverse problem above.

**Data/Model → Prior.** Training biological foundation models on heterogeneous, context-rich data — integrating sequence, structure, surface chemistry, evolutionary signals, and experimental readouts — so the model learns to condition on the full biological context rather than any single modality alone.

**Prior → Data.** Closing the loop: using the neural prior's uncertainty to guide experimental design and enable efficient, AI-centric data collection. This is the frontier I aim to develop alongside experimental collaborators.
