# MIPS 1 

### Recap: 
- 32 bits for the data width
- Stages: IF, ID, EX, MEM, WB
- Control unit 

### Instructions:
```
;replace r1 with rs and r2 with rd
ADD $r1, $r2, $r3
SUB $r1, $r2, $r3
MUL $r1, $r2 ;predefined destination registers
INC $r1
DEC $r1
AND $r1, $r2, $r3
XOR $r1, $r2, $r3
OR $r1, $r2, $r3
NOR $r1, $r2, $r3
SLL $r1, sa, $r2
ADDI $r1, imm, $r2
SUBI $r1, imm, $r2
LD  
ST
JMP imm ;destination address
```

### R-Type

|Opcode|Rs|Rt|Rd|sa|func|
|-|-|-|-|-|-|
|6|5|5|5|5|6|

### I-type

|Opcode|Rs|Rt|imm|
|-|-|-|-|
|6|5|5|16|

### J-Type

|Opcode|imm|
|-|-|
|6|26|


## RTL Abstracts

|Instruction|RTL Abstract|Program counter|
|-|-|-|
|add $rs $rt, $rd|RF[\$rd] $\leftarrow$ RF[\$rs] + RF[\$rt]|PC $\leftarrow$ PC + 1|
|mul $rs $rt $rd|RF[\$r1] $\leftarrow$ hi(RF[\$rs] * RF[\$rt])|PC $\leftarrow$ PC + 1|
|still mul|RF[\$rd] $\leftarrow$ lo(RF[\$rs] * RF[\$rt]) |-|
|inc $rs|RF[\$rs] $\leftarrow$ RF[\$rs] + 1|PC $\leftarrow$ PC + 1|
|sll $rs $rt sa|RF[\$rt] $\leftarrow$ RF[\$rs] << sa|PC $\leftarrow$ PC + 1|
|addi $rs $rt imm|RF[\$rt] $\leftarrow$ RF[\$rs] + S_EXT(imm)|PC $\leftarrow$ PC + 1|
| subi|||
|ld \$rt, imm|RF[\$rt] $\leftarrow$ Mem[Ext(imm)]||
|st $rs, imm|Mem[Ext(imm)] $\leftarrow$ RF[$rs]|
|jmp imm||PC $\leftarrow$ PC + 1 + Ext(imm)|


## Machine code

|Instruction|Encoding|
|-|-|
|add|000000_sssss_ttttt_ddddd_00000_000000|
|sub|000000_[...]\_000001|
|...|...|
|sll|000000_[...]\_001001|
|addi|000001_[...]|
|jmp|000101_[...]|

> [!info] For Inc
> - in RTL abstract we can take the rt to be overwritten

## Design

### Instruction Fetch
- PC (implement as counter/register)
	Ports (in as default)
	- CLK
	- Reset (linked to board BTN)
	- PC + 1
	- Load
	- Enable (will be linked to board BTN)
- Adder
- Instruction Memory (ROM)
	- Address (32)
	- Data (out) (32)

### Instruction Decode 
- Register File
	Inputs:
	- ra1
	- ra2
	- wa1
	- Wd1
	- wa2
	- Wd2
	- write enable1
	- write enable2
	- read enable (for jump)
	Outputs:
	- rd1
	- rd2


### Execution Unit
- ALU
	- MUX for second input
	- ALUControl for generating ALU operation
- Extension Unit

# To Do
- implement (extend previous MIPS for 32 bits)
- put on board for 10