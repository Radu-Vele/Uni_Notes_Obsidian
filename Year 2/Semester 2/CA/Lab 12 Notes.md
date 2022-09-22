---
tags: [Notebooks/CA]
title: Lab 12 Notes
created: '2022-05-13T11:10:55.032Z'
modified: '2022-05-13T12:10:15.399Z'
---

# Lab 12 Notes

# Words on the exam

# CPU Performance

- speed it up
- instead of frequency increase, paralellism has been introduced

# Lecture Recap:

- single cycle - discussed in the labs 4-8

## Multi cycle: Steps (a part of the MIPS is called a *phase*)

  1. ISA Definition -> Abstract RTL (register-transfer-level)

  2. Data-path

  3. Reorganize Data-Path

  4. Concrete RTL

  5. Concrete RTL -> Control (take a look at a component in a step); 
  - instructions take from 3-5 cycles (all instructions use from 3 to 5 phases)

  - control signals determine the correct result => table for the control signals => try to make it optimal ish => Hardwired Unit / Micro-programmed

a. Hardwired implementation 
- after implementation, can't be modified
- used for critical fields (med, military, etc.)

b. Microprogrammed
- easy to repurpose
- used more often (cheaper)

- implementation of a & b in slides (L7)

## Pipeline
> Critical path = longest propagation time between two registers (instruction that takes the longest time)

> Throughput = nr instr/time interval

- create a pipeline:
  - take the longest instruction and divide it into multiple 
  - **balance length** between the stages
  - introduce registers between the phases => 5 simultaneous instructions for each clock cycle (aim)
  - check how many bits each register needs to accomodate
  - problem: ***write address*** needs to be transported through the pipeline
  - careful about control signals => need to be transported as well (e.g. the **MemRead** signal is not used in the lab) (not all of them, but only the ones used in the later stages)

### Hazards :volcano:
1. Structural
- use the same resources by 2 instr
2. Data
- data use before ready
3. Control (flow)
- branch / jump related

- Described in the lecture.

### Our lab goal: 
Same behavior between the single cycle and pipeline implementations. => *Add NoOps*

