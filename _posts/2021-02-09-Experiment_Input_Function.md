---
layout: post
title: Experiments on Input Functions
tags: BiologicalComplexity 
katex: True
progress: 100%
---

This is a summary of papers on experimental investigations of gene's input function, especially about [*Diverse Two-Dimensional Input Functions Control Bacterial Sugar Genes (2008)*](https://pubmed.ncbi.nlm.nih.gov/18374652/) and [*Plasticity of the cis-Regulatory Input Function of a Gene (2006)*](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.0040045). 

Living cells are capable of responding to the environment conditions, or signals, in various ways. One important choice is regulating gene expression. The relation between the level of input signals and the transcription rate of the gene is called the gene’s input function. Clarifying the form of input functions is crucial in understanding the gene regulation and further evolution. As most genes are regulated by multiple signals, these papers reported well-designed experimental platforms to present the diversity of two-dimensional input functions, providing solid background for further theoretical abstrction. 
<!--more-->

Generally speaking, the Gene's input function is biological computation circuits that take in multiple signals and output some gene expression levels. Intuitively, we can sketch those input functions by simultaneously recording their taking-in signals and output levels. The bio-flourescent tools developed after 2000s[^1] made the experimental accurate measurement of gene expression level in living cells possible, while the signal levels as external conditions can be measured accordingly. Thus, we can see how those input functions look like in real living cells. 

Model system used in 2006 paper are lac operon variants  from E. Coli, where each variant contained 3 to 9 point mutations (a very small number given the total base number) compared with wild type. Two controlled signals are cAMP and isopropyl-D-thiogalactoside (IPTG)  concentrations. The outputs, gene expression levels, is measured from the fluorescence in living cells strains with those variants. Main results are represented by the following Figure 4 in origin paper:  two-dimensional input functions of all *lac* variants, where two axes correspond to the two signal concentration levels, and the color means the gene normalized gene expression level. 

<center><img src="https://raw.githubusercontent.com/minhuanli/imagehost/master/img/Screen%20Shot%202021-02-10%20at%205.49.53%20PM.png" style="zoom:40%;" /></center>

The authors interpreted those functions in a Boolean manner. At least two important obcservations from the results:

1. The types of input functions are diverse, including OR-like (row A) gate, single-input switch (row B), AND gate (row C and row D)
2. Several point mutations are already capable of changing the input funtion type.

Similar conclusions are also concluded in 2008 paper, where the researchers used promoters from five different E.Coli. sugar systems as model system. The two controlled signals are external sugar and cAMP concentration. Again, gene activity is the rate of GFP fluorescence accumulation per OD unit in exponential phase. Here it the results (Figure 2 from origin paper). 

<center><img src="https://raw.githubusercontent.com/minhuanli/imagehost/master/img/Screen%20Shot%202021-02-10%20at%205.50.20%20PM.png" style="zoom:40%;" /></center>

Despite the authors now interpret the input functions as real-value functions instead of Boolean ones, observations are similar:

1. The two-dimension input function are of truly diverse shapes.

2. Some of the input functions are nonmonotonic, peaking at intermediate signal levels. (see first and third panel on second column)
3. Most of the input functions show separation of variables, in the sense that they can be described as the product of simple functions that depend on a single input.

The diverse shapes of input functions are really fascinating for further evolutionary algorithmic discussions, especially given the fact that such diversity can be explored with only several point mutations. 

### References

[^1]: Setty Y, Mayo AE, Surette MG, Alon U (2003) Detailed map of a cis- regulatory input function. Proc Natl Acad Sci U S A 100: 7702–7707.

