---
layout: post
title: Facilitated Variation
tags: BiologicalComplexity 
katex: True
progress: 100%
---

This is a summary about paper *Gerhart, John, and Marc Kirschner. "The theory of facilitated variation." PNAS (2007)*. It is a paper proposing a direct but quite heuristic thoery to explain the "variation" in the evolution. It have long been a mystery that, in Darwin's theory of evolution, how rare and random mutation can lead to exquisite changes of form and function. Some key advances regarding developmental biology, like how genetic information is transmitted to the next generation, how this information is recovered to produce the active components of cells, have revealed how a single-celled egg develops to a functional adult. Such new insights have permitted the emergence of the new thoery. My summary has borrowed a lot from Ana's CS229r presentation and *An interview with Marc Kirschner and John Gerhart*.<!--more-->

In the course of their descent from a common ancestor, animals have diverged in their anatomy and physiology by the gradual accumulation of selected heritable modifications, their phenotypic variations. How does genetic change result in such a variaty of pehnotypes remain the most mysterious part of Darwin's theory of evolution. The authors made a center claim that the facilitated variation is achieved by **conserved core components** and **evolved regulation**. They argued that conserved core processes greatly facilitate the animal's generation of complex variation by reducing the number and kind of regulatory changes needed and hence the number of random mutational changes needed in the genome. So variation is not as hard to get as one might initially think, like "The same Lego parts can be stuck together to give a model of the Eiffel Tower or of a soccer ball." 

The core compoents are those fundamental processes operating the animal's phenotype. These "toolkit" components are largely unchanged across different creatures. And they demonstrate modularity and are largely reused. For example, 79% of mouse genes are reused from prokaryotes, plants, fungi and other animals. And we humans even share ~45% DNA with bananas. 

However, those conserved core components are linked, by regulatory means, in different combinations. They authors made a special arugement about the linkage, that the conserved core processes have a special capacity for **weak regulatory linkage**, which means only few instructions can alter such linkages easily. Generally, the responding core process can produce the output by itself but inhibits itself from doing so. The regulatory signal mearly interferes with the self-inhibition (the intermediate agency), thus releasing the output. So core processes are self-inhibit and the regulatory signal just triggers the output. So the signal itself can not be so complex. A simple example is the allosteric proteins: they can switch between on/off states and mostly off by default. Regulatory agents, some ligands, can bind strongly to the preferred state and stabilize that state, as an activator or an inhibitor. So **states of core processes are built in, regulators just pick one**. 

Then come the **exploratory processes**, also quite directive. The conserved core processes can search & find targets through variation and selection. Variation step means they generate a ton of output states (like a energetic probability distribution). In the selection step, some regulateory agents will choose and stabilize the preferred outputs. 

The conserved core components, weak regulatory linkage and exploratory processes consist the key idea of the facilitated variation thoery.
