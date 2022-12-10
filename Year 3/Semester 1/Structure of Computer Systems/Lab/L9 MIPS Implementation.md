# MIPS Multi-Cycle Implementation

## IF
- extend signals to 32 bit
- exclude branch
- [x] Done

## ID
- modify len
- modify extension unit
- [x] Done

### Register File
- extend signals
- add enable for writing to 2 registers (write before read - use a variable in the process)
- add enable for reading
-  [x] Done

## EX
- adapt ALU for our operations
- eliminate ALUOp unit
	- [x] Done
- [ ] shift and make sure to have all operations

## MEM
- add read enable and synchronous reading
- [x] Done

## WB
- nothing much different
- [x] Done

![[Pasted image 20221205171611.png]]

### Toplevel
- guide: the upper drawing - but don't use the same memory
- instance of the components
- add registers
- [x] Done
- figure out the role of every component
- [x] Done
## Testing
- test program provided
![[instructions.jpg]]

Test
- [x] Testing in simulation

|Instruction|Tested ok | Remarks|
|-|-|-|
|R-type|Y|Had to do synchronous register read on falling edge|
|MUL|Y||
|I-type|Y||
|LD|Y|I should change the FSM s.t. it jumps from ID to MEM|
|ST|Y|-||The actiond to memory are done on the fallin edge|
|Jump|Y|Should change to compute the jump address in EX unit


> [!info] Status:
> - have a functional MIPS, but to be a classical multi cycle a few more modifications need to be done:
> 	- merge memory `[ ]` 
> 	- eliminate the adder from the IF unit `[ ]` 
> 	- change the control for loading to go from ID to MEM `[x]`
> The undone ones are subject of future implementations 👴

### Other multi cycle improvements
- single memory
- next pc computed in the alu