---
tags: [Notebooks/CA]
title: Lab 6.0 MIPS Instruction Decode + CTRL unit
created: '2022-03-25T08:18:26.702Z'
modified: '2022-03-25T12:37:22.983Z'
---

# Lab 6.0 MIPS Instruction Decode + CTRL unit

## Instruction Decode 
- make sense of the given instruction
- Reg File `instantiate the one we worked with trough lab3`
- MUX
- Sign/Zero Ext

|Input|Output|
|-|-|
| Instr (15 downto 0) | RD1|
| RegWrite | RD2|
| RegDst | Ext_imm (15 downto 0)|
| ExtOp | func (2 downto 0)|
| WD | sa (shift_amount)|
|clk100MHz||

## Main Control Unit
- set corresponding control for each instruction (lecture 4 slide 24 example)
- Input: Instr(15 downto 13) = opcode
- Outputs on one bit + ALUOp on more bits: ctrl signals RegDst, ExtOp, ALUSrc, Branch, Jump, ALUOp, MemWrite, MemtoReg, RegWrite
- maximum 3-4 instructions in main control unit 

### Implementation: a simple case / if's based on opcode 

- can create a separate file / separate

## TO DO :computer:

1. ID design (new entity) (for Reg file we can use the previously designed component) :white_check_mark:
    - WD is reused from the sum of the two RD values and loop back to WD (lab 3 like)
2. Main control unit design 
    - identify control signals for my instructions (lab 4 + lect 4)
    - table with control signals (for 4-6) instructions

3. Test ID + Control Unit
    - instantiate in test_env
    - ID unit + RD1 + RD2 trough Adder
    - Register Write => control through a button (in an AND gate with RegWrite signal)
    - control SSD input using sw(7:5)
    - LED display ctrl unit signals (8 downto 0)
    - branch and jump hard-coded like in prv lab
