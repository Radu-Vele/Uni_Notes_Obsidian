---
tags: [Notebooks/CA]
title: Lab 4.1 (Hw)
created: '2022-03-12T08:54:34.596Z'
modified: '2022-03-18T13:48:48.740Z'
---

# Lab 4.1 (Hw)
## Assignment 1:
Starting from the instruction formats presented in the previous section write the instruction format (on bits, including the opcode and function fields) for each of the instructions presented in Table
### R-Type instructions
---

|Instruction| Format | RTL Abstract|
|-|-|-|
|Addition|B"000_001_010_011_0_001"| RF[rd]<-RF[rs] + RF[rt]|
|Subtraction| B"000_001_010_011_0_010"| RF[rd]<-RF[rs] + RF[rt]|
|Shift Left Logical|B"000_001_010_011_1_011"|RF[rd]<-RF[rs] << 1 |
|Shift Right Logical|B"000_001_010_011_1_100"| RF[rd]<-RF[rs] >> 1|
|Logical AND|B"000_001_010_011_0_101"|RF[rd]<-RF[rs] & RF[rt]|
|Logical OR|B"000_001_010_011_0_110"|RF[rd]<-RF[rs] OR RF[rt] |
|****Logical XOR***|B"000_001_010_011_0_111"|RF[rd]<-RF[rs] ^ RF[rt] |
|****Shift Right Arithmetic***|B"000_001_010_011_1_000"|RF[rd]<-RF[rs] >> 1 (with S_EXT)|
(\*) additional instructions

### I-Type instructions
---
|Instruction| Format | RTL Abstract| 
|-|-|-|
|Add Immediate|B"001_001_010_0001001"|RF[rt]<-RF[rs] + S_EXT(x"09")| 
|Load Word|B"010_001_010_0000010"|RF[rt]<-M[RF[rs] + S_EXT(x"02")]|
|Store Word|B"011_001_010_0000011"|M[RF[rs] + S_EXT(x"03")]<-RF[rt]|
|Branch on Equal|B"100_001_010_0000101"|*if* (RF[rs] = RF[rt]) *then* PC<-PC+4 + S_EXT(x"05") << 1|
|****Branch on Less than Zero***|B"101_001_010_0000011"|*if* (RF[rs] < 0) *then* PC<-PC+4 + S_EXT(x"05") << 1|
|****Load Upper Immediate***|B"110_001_010_0011100"|RF[rt]<-x"01C" \\\ x"00" |

### J-Type instructions
---
|Instruction|Format|RTL Abstract|
|-|-|-|
|Jump|B"111_0000000000100"|PC<-x"04"|

## Assignment 2

Write a short program with the instructions that you have defined for your MISP 16 processor. Describe the program in assembly language, then each instruction in machine code (16-bit encoding for each instruction, use “_” between the fields of the instructions).

### Test program
---
|Line|Assembly| Machine code|
|-|-|-|
|1|lw $rt, $imm(\$rs)|B"010_001_010_0000010"|
|2|lui $rs x"1C"|B"110_001_001_0011100"|
|3|sra $rs, $rt, sa|B"000_001_010_001_1_000"|
|4|add $rd, $rs, $rt|B"000_001_010_011_0_001"|
|5|beq $rs, $rt, x"3"|B"100_001_010_0000011"|
|6|sub $rd, $rs, $rt|B"000_001_010_011_0_010"|
|7|sw $rt, x"3"(\$rs)|B"011_001_010_0000011"|
|8|xor $rd, $rs, $rt|B"000_001_010_011_0_010"|
|9|sw $rt, x"4"(\$rs)|B"011_001_011_0000100"|
|10|or $rd, $rs, $rt|B"000_001_010_011_0_110"|
|11|sw $rt, x"4"(\$rs)|B"011_001_011_0000100"|


### Test program 2 Calculates the n-th Fibonnaci number
  - the index of the fibonnaci number desired is stored in the register 1001
  - we need two previous variables
  - the result is written in rd
```
//pseudocode
if(index == 0 or index == 1)
  result = index; //keep result in 100;

prv = 0; //prv is 010
result = 1;

while index < desired_index:
do 
  ax = result; 
  result = ax + prv;
  prv = ax;
  index++;
done;
```
---
|PC Address|Assembly| Machine code|
|-|-|-|
|0|

## Assignment 3
---

 inDraw the Data-Path of your single-cycle MIPS 16 processor. Be sure to include all the necessary components on the data-path, such that all the 15 instructions execute correctly.

---
### MIPS Data path:

<p align="center">
  <img src="@attachment/MIPS_1.jpg" width="2000">
</p>

---

