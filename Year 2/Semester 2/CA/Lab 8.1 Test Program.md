---
tags: [Notebooks/CA]
title: Lab 8.1 Test Program
created: '2022-04-08T11:06:34.038Z'
modified: '2022-05-13T12:48:15.507Z'
---

# Lab 8.1 Test Program

## Quiz :clock130:  
- 14:05 start
- past 4 laboratory SC MIPS 16
- know everything about MIPS implementation 
(e.g:
  - implement a mips based on an instruction set
  - 5 phases )


# Test Program MIPS 16 Single Cycle :page_facing_up:
```C
//Test program assembly
// target: MIPS 16 Single Cycle
// description: Program that loops through an array of 7 numbers and counts how many of them are even

// We will hard-code into memory the values of the array starting at address x"0000 0001"

// empty up the registers just in case
xor $1, $1 ; //count put into the register file
xor $2, $2 ; //iterator
xor $4, $4 ; //a value to or with an array value for comparison
xor $5, $5 ; //value to compare to to check if even
xor $6, $6 ; //end the iteration

addi $2, x"0001" ; //initiallize r010 with value 1
addi $4, x"FFFF" ; //initiallize the value of $100 with x"FFFF"
addi $5, x"FFFE" ; //initiallize the value of $5 with x"FFFE"
addi $6, x"0007"	; //value for loop termination - init with nr of iterations

add $6 $2 ; //the nr of iterations is added the initial value of the iterator

label_loop:

	lw $3, MEM[$2 + 0] ; //load next element
	or $3, $5 ; //store the result in $3 -- create a number that will be x"FFFE" if even or x"FFFF" if odd
	
	beq label2 $3, $4 ; //branch if the number is odd
	addi $1, 1; //increment counter for even numbers

	addi $2, 1 ; //increment iterator -- step here from beq

beq $2, $6 ; //finished loop => skip the jmp instruction
jmp label_loop ; //loop again 

addi $1, x"0000" ;// store the result in $1 to see it on the development board 
``````

### Instruction encoding

PC Line|Instruction|Encoding|Remarks|
|-|-|-|-|
0|xor $1, $1, $1 | B"000_001_001_001_0_111"
1|xor $2, $2, $2 | B"000_010_010_010_0_111"
2|xor $4, $4, $4 | B"000_100_100_100_0_111"
3|xor $5, $5, $5 | B"000_101_101_101_0_111"
4|xor $6, $6, $6 | B"000_110_110_110_0_111"
5|addi $2, $2, x"0001"| B"001_010_010_0000001"
6|addi $4, $4, x"FFFF"| B"001_100_100_1111111"
7|addi $5, $5, x"FFFE"| B"001_101_101_1111110"
8|addi $6, $6, x"0007"| B"001_110_110_0000111"|IF() stage -> WB()available in 4 cycles
|9|NoOp|
|10|NoOp|
|11|NoOp|
|12|add $6, $6 $2 | B"000_110_010_110_0_001"|IF() stage, $6 needed in ID (1 cycle from now)|
|13|lw $3, MEM[$2 + 0] | B"010_010_011_0000000" | IF() stage -> WB in 4 clock cycles 
|14|NoOp|
|15|NoOp|
16|NoOp|
17|or $3, $3, $5| B"000_011_101_011_0_110" | IF() stage -> $3 needed in one cycle from now, new $3 available in 4 cycles|
18|NoOp|
19|NoOp|
20|NoOp|
21|beq label2 $3, $4| B"100_011_100_0000001" |IF(stage) -> $3 needed in the next cycle|
22|NoOp| --> no op after branch
23|NoOp| -- \| \| --
24|NoOp| -- \| \| --
25|addi $1, $1, 1| B"001_001_001_0000001"
26|addi $2, $2, 1 |B"001_010_010_0000001"
27|beq $2, $6| B"100_010_110_0000001"
28|NoOp| --> no op after branch
29|NoOp| -- \| \| --
30|NoOp| -- \| \| --
31|jmp label_loop| B"111_0000000001101" |--> jump to lw
32|NoOp| --> no op after jump
33|addi $1, $1, x"0000"| B"001_001_001_0000000"
