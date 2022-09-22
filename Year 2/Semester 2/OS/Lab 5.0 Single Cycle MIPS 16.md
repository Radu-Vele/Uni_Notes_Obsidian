---
tags: [Notebooks/CA]
title: Lab 5.0 Single Cycle MIPS 16
created: '2022-03-17T15:05:33.191Z'
modified: '2022-03-18T13:20:18.600Z'
---

# Lab 5.0 Single Cycle MIPS 16

## Instruction Execution Cycle
```mermaid
graph LR
IF[Instruction Fetch]-->ID/OF[Instruction Decode / Operand Fetch]-->EX[Execute]-->MEM[Memory]-->WB[Write-Back]
```

## Mips organization:
- 5 modules (different entities) $\in$ test_env.xpr
- this lab ***Instruction Fetch Unit***

### Instruction Fetch Unit:
---
- Program counter (is actually a D-FlipFlop)
- Instruction Memory (ROM)
- Adder (with 1)
- a few mux for determining the address of the next PC
- all the data fields are 16 bits wide
- use a subset of the program counter address (16) i.e. take the LS8B (7:0)

INPUTS:
1. Jump_Address
2. Branch_Address
3. Clk
4. Jump Ctrl Signal
5. PCSrc Ctrl Signal

OUTPUT:
1. Instruction
2. Next PC address

## TODO:

- Prepare the 15 instructions from the previous lab + ROM in the test_env alognside the test program in machine code

1. Design VHDL IF Unit  (IF Entity with no other components declared inside of it)

2. Test IF Unit (Instatiated IF in the test_env + ssd + mpg)
    - In the ROM we put some instructions from last lab
    - For the next week add the proper values
    - Branch Address should be within the range of the input instructions

3. Machine code that does something

## Q's
- what was branch?
