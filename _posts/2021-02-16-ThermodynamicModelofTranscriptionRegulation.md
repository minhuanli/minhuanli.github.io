---
layout: post
title: Thermodynamic model of transcription regulation
tags: BiologicalComplexity 
katex: True
progress: 100%
---

This is summary about paper [*Bintu et al. (2005) Transcriptional regulation by the numbers: models*](https://www.sciencedirect.com/science/article/pii/S0959437X05000304?casa_token=0Bmq59nIMvgAAAAA:sJDfmyWysX19tjo7KJ17tLd3PWFMcUitP6s4J66tKUTucrNYFp-SuiXX5c8tDKqjBk_a8J4wmLc). The authors established a statistical mechainics model to quantitatively understand the initiation of DNA transcription, through the probability of RNA polymerase binding at the promoter of interest. This summary borrows a lot of ideas from Anastasia Ershova's presentation at CS229r course. 

The fundamental information flow in the biology systems is fascinating: information saved in DNA as 1D sequence will be transformed into proteins with 3D structures and operate functions. There is a central dogma controlling the protein expression levels, with two general forward steps: first is transcription, RNAs are constructed based on regulated transcription; second is translation, RNAs are translated into proteins. Each step consists of three stages: Initiation, Elongation and Termination. The intiation is marked by a RNAP molecules bind to the promoter gene. Based on the knowledge, the authors build a theoretical framework to quantitatively understand the gene expression level, based on equilibrium statistical mechanics.<!--more-->

Say, there are $$P$$ RNAP molecules, $$N_{NS}$$ non-specific sites, and one single promoter site. The P RNAP molecules can each bind to either non-specific sites or the promoter site. If promoter site is bound, the transcription process is considered as start. So ideally, the expression level can be modelled as the probability of RNA polymersa binding at the promoter of interest, which is a solved problem in equillibrium statistical mechanics.

We consider two conditions:

1. All $$P$$ RNAP bound to the non-specific promoters, the statistical weight is :
   
   $$
   \underbrace{Z(P)}_{\text {tatistical weight-promoter unoccupied }}=\underbrace{\frac{N_{N S} !}{P !\left(N_{N S}-P\right) !}}_{\text {number of arrangements }} \times \underbrace{e^{-P \varepsilon_{p d}^{N S} / k_{B} T}}_{\text {Boltzmann weight }}
   $$
   

   simply from combinatorics calculation plus equilibrium assumption, $$\varepsilon^{NS}_{pd}$$ is an energy that represents the average binding energy of RNAP to the genomic background. 

2. $$P-1$$ RNAP bound to non-specific promoters and one RNAP bound to the promoter of interest, which means the transciption starts:
   
   $$
   Z(P-1) e^{-\varepsilon_{p d}^{S} / k_{B} T}
   $$

    where $$\varepsilon_{p d}^{S}$$ is the binding energy for RNAP on the promoter. 

Then the total statistic weight is:

$$
\underbrace{Z_{\text {tot }}(P)}_{\text {total statistical weight }}=\underbrace{Z(P)}_{\text {promoter unoccupied }}+\underbrace{Z(P-1) e^{-\varepsilon_{p d}^{S} / k_{B} T}}_{\text {RNAP on promoter }}
$$

Thus, the probability of RNAP bound to promoter, which is viewed to proportional to the expression level, is:

$$
p_{\text {bound }}=\frac{Z(P-1) e^{-\varepsilon_{p d}^{S} / k_{B} T}}{Z_{\text {tot }}(P)} \approx \frac{1}{1+\frac{N_{N S}}{P} e^{\Delta \varepsilon_{p d} / k_{B} T}}
$$

where $$\Delta \varepsilon_{p d}=\varepsilon_{p d}^{S}-\varepsilon_{p d}^{N S}$$ is the binding energy difference, and we assume $$P \ll N_{NS}$$ to obtain the final expression. 

Futheremore, some activities with rea-life meaning, like fold-change to the promoter, can be incorporated into the framework as a regulation factor $$F_{reg}$$:

$$
p_{ bound }=\frac{1}{1+\frac{N_{N S}}{P F_{r e g}} e^{\Delta \varepsilon_{p d} / k_{B} T}}
$$

The regulation factor should be seen as describing an effective increase (for $$F_{reg} > 1$$) or decrease (for $$F_{reg} < 1$$) of the number of RNAP molecules that are available to bind the promoter.

The model result itself is beautiful, but we have to review all its assumption to see if it really makes sense. 

1. Equilibrium 

   This is the basis of the whole energy-based discussion, but also the most problematic one. Equillibrium is kind of a strict condition, whic requires ergodicity, detail balance, equpartition, no non-thermal energy input... It is hardly to believe such a complex bilogical process is at equillibrium. Instead, from the famous Hopfield's Kinetic proofreading model, we know that to correctly understand the error rate of DNA replication, a dynamic model considering the external energy input is necessary. 

2. $$P_{bound} \propto$$ expression level

   This is true somtimes in prokaryotes, but almost never in eukaryotes due to downstream regulation. 

3. Transcription apparatus is a single molecule (only considering RNA polymerase - RNAP):

   This is still not true but not fatal. Most transcription appratus are a complex (loads of factors in eukaryotes), but same analysis framework with additional factors may still work.

4. All RNAP is bound to a promoter (either promoter of interest or "nonspecifically")

   This is again not true, especially when you assume there are fix number of RNAP! There are lots of free-floating RNAP as well. Combinatorics the framework is built on are confounded - likely far more non-bound states.

5. All factors being considered act independently (no cooperativity)

   Not true! Lots of cooperativity (positive and negative) in factor binding and recruitment

Given nearly all the assumptions are questionable, can this model still be considered informative? Even though it might correspond with some experiemental data. 