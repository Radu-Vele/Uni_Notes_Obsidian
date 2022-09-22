---
tags: [Notebooks/CA]
title: Lab 7.0 MIPS Execution Unit (ALU)
created: '2022-04-01T07:28:49.904Z'
modified: '2022-04-01T11:05:53.020Z'
---

# Lab 7.0 MIPS Execution Unit (ALU)
# Week 9 2nd Quiz :smile:

- based on Single Cycle MIPS

Update - we can take encoding instruction and get the control signals

## 1. Execution Unit
Components:
- ALU
- ALU control
- Mux
- Shift Left 2 and adder for the branch target address

Inputs:
- RD1 (16 bit)
- RD2 (16 bit)
- Ext_Imm (16 bit)
- ALUSrc (1 bit)
- sa (1 bit)
- func (3 bits)
- ALUOp (2 bit)
- PC + 1 (address - 16 bit)

Outputs:
- Branch Address (16 bit)
- Zero (detected) (1 bit)
- ALURes (16 bit)

## 2. ALU control unit
- defines ALU operations
a. R-Type -> ALUCtrl is defined by the fixed value ALUOp and function field
b. I-Type -> ALUCtrl is defined by the ALUOp simply

## Questions:
- table control signals ?
- extension unit - one liner ?

## TODO:
1. Design Instruction Execution Unit
    - new component
    - in the new component implement behavioral
    - branch target address - one line of code
    - process with case for ALU
    - process for ALUControl 

2. Test Execution Unit
    - instantiate execution unit
    - connect ALURes to WriteData port of ID unit
    - test all instructions
    - Output: sw(7:5) (described in ppt)
    - LEDs: control signals from Main Ctrl Unit
