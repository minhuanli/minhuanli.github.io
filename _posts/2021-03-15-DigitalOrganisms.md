---
layout: post
title: Digital Organisms
tags: BiologicalComplexity 
katex: True
progress: 100%
---

This is a summary about paper *Lenski et al. "The evolutionary origins of complex features",  Nature 2003*. They authors used a novel experimental system, digital organisms, to explore the ability of organisms to evolve complex functions. They demonstrated the power of random mutation (even deleterious) and natural selection in the evolutionary pathway to complex functions.

A long-standing challenge to evolutionary theory has been whether it can explain the origin of complex organismal features, given the extinction of intermediate forms, imperfection of the fossil record, and incomplete knowledge of the genetic and developmental mechanisms that produce such features. To tackle this issue, the authors performed experiments with digital organism on Avida platform. Digital organisms are self-replicating computer programs that can mutant ramdomly and evolve spontaneously. They also compute for energy and realize logic functions by a series of instructions.<!--more-->

Here is a breakdown of the digital organisms:

1. Each organism has a circular genome. A genome is a circular sequence of instructions, each instruction is one of 26 possible instructions (instructions are operations over the data in stacks and registers). Each orgnism has a virtual CPU with two stacks and 3 registers that hold 32-bit strings. 

   - `nand` are the only logical operator in the instruction set, it perform a bitwise NAND on the values in two registers. NAND is a complete logical operator. 
   - `IO` (‘input–output’) is the instruction to output the value in a register and replace with a new input. It is essential to get the reward. 
   - A serials of instructions will be combined to perform a logic operator and then get the energy reward. For example, `nand` must be executed in coordination with `IO` (‘input–output’) instructions to perform the NAND function

2. When an organism copied its genome and divided, the resulting offspring was randomly placed in one of the eight adjacent cells or in the parent’s cell. Each birth caused the death of the individual that was replaced, thus maintaining a constant population size.

3. Errors like point mutations (0.0025 errors per instruction), insertions (0.05 per genome copied) and deletions (0.05 per genome copied) can happen during the replication; In general, 0.225 mutations are expected in a genome of length 50. 

4. Digital organisms compete for the energy (in the quanta called SIP) needed to execute instructions. Each SIP suffices to execute one instruction. There are two energy sources:

   - Each organism receives SIPs in proportion to its genome length.
   - An organism can obtain further SIPs by performing one- and two-input logic operations on 32-bit strings

   Total enegy equals to the product of its genome length and computational merit

The rewards for performing logic functions are shown in the following table 1:

<center><img src="https://raw.githubusercontent.com/minhuanli/imagehost/master/img/image-20210227215950127.png" style="zoom:40%;" /></center>

The authors started with 3,600 identical copies of an ancestral genotype that could replicate but could not perfomr any logical functions. Environment is a lattice with a capacity for 3,600 individuals. The evolution target is the `EQU` function. These settings reads truly complex, but we can try to summarize it into few key points and make an analogy with biological contexts:

1. Complex functions in biological organisms correspond to logical operators in digital organisms, realized by a series of instructions
2. Genotypes correspond to serial instructions in digial organisms, and their replication and mutations are also mimicked.
3. A digital organism’s expected reproductive rate, or fitness, equals its rate of energy acquisition divided by the amount of energy needed to reproduce.  This would guide their evolution to more and more complex logical functions.

And the results from this setting can be summarized into the follwoing takeaways:

1. The evolution of the complex `EQU` function is realatively likely (23 of 50 trials) with such mutation and natrual selection principles. But an particular pathway is unlikely. And more interesting, if less intermediate fucntions are rewarded, or only the final `EQU` function is rewarded, then final `EQU` function will evolve much less often. 

2. The evolution of a complex feature is not always an upwards climb to a fitness peak, but instead may involve critically important backwards and sideways steps.
