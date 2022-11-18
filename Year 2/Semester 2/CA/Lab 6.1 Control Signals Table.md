---
tags: [Notebooks/CA]
title: Lab 6.1 Control Signals Table
created: '2022-03-25T12:03:16.161Z'
modified: '2022-04-07T13:59:03.237Z'
---

#  Lab 6.1 Control Signals Table

## Control signals table (For Main Control Unit)

|instruction|opcode|RegDst|ExtOp|ALUSrc |Branch|Jump|ALUOp|MemWrite|MemtoReg|RegWrite|
|-|-|-|-|-|-|-|-|-|-|-|-|
|***R-type***|-|-|-|-|-|-|-|-|-|
|add|000|1|0|0|0|0|10|0|0|1| 
|sub|000|1|0|0|0|0|10|0|0|1|
|sll|000|1|0|0|0|0|10|0|0|1|
|srl|000|1|0|0|0|0|10|0|0|1|
|and|000|1|0|0|0|0|10|0|0|1|
|or|000|1|0|0|0|0|10|0|0|1|
|xor|000|1|0|0|0|0|10|0|0|1|
|sra|000|1|0|0|0|0|10|0|0|1|
|***I-type***|-|
|addi|001|0|1|1|0|0|00|0|0|1|
|lw|010|0|1|1|0|0|00|0|1|1|
|sw|011|x|1|1|0|0|00|1|0|0|
|beq|100|x|1|0|1|0|01|0|0|0|
|blz|101|x|1|0|1|0|01|0|0|0|
|lui|110|0|1|1|0|0|11|0|0|1|
|***J-type***|-|-|-|-|-|-|-|-|-|
|jmp|111|x|x|1|0|1|00|0|0|0|

Remark: for LUI we need to add another operation in the ALU
