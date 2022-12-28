# Implementation 2

Present the working code using some testbenches
- [x] Done - fibonnaci may do the job ok

Modified documentation:
	Figure out how to integrate pretty stuff from Tudor
- [x] Done

## Re-organize the code when needed 
> [!warning] Should be rested when doing this 🙂

- rearrange signals, rename when stupid names were given
- resize pipeline registers (though stuff)
	- will do it in the end
- check for any poorly written section
- [x] Added TODOs for the end

## Correct aspects related to the design chapter that do not hold anymore

#### 1. Correct Fig 4.2
- MUX that selects the immediate or register data for ALU input 2 needs to be the closest one to ALU
- [x] Done
- [x] Added to documentation

#### 2. Add `BNEQ` instruction to table 4.1
- [x] Done

#### 3. Modify 4.7 
- to have accurate inputs of BHT and a mux with 4 entries instead of the one that has as selection FLUSH
- add correct inputs to BHT
- add the mechanism for `bneq`
- [x] Done
- [x] Added to documentation

#### 4. Modify 4.5
- only 2 inputs to mux for forwarding
- add instruction input to fwd unit
- [ ] Done
- [x] Added to documentation

## Add Implementation Chapter + Code
- insert code from the implemented components

#### Modifications to MIPS pipeline implementation initial
- removed some instructions
- read from the register file on the falling edge
- add jump computation to IF
- [x] Done

#### EX Forwarding
- forwarding unit implementation add
- [x] Done

#### MEM Forwarding
- implementation
- add `WB_Buf` - mention
- [x] Done

#### HDU Load data hazard
- implementation

#### Branch move to ID
- flush generation
- can put all ID unit there

#### BHT implementation
- implementation

#### HDU extension 
- for additional stalls and Forwarding to ID for detecting branch conditions
- add implementation

## Add testing chapter
- not necessarily before monday, but it would be useful to write some tests while I do the testing myself
- prepare a master program to test many hazard solutions (Fibonnaci or so)

>[!question] Questions
>- Did I add too much code?
>	- `I should add no code, maybe just some data structures or so - move the details regarding input/outputs to the` implementation `chapter and keep just diagrams and brief mentioning into the` Design `chapter`
>- How should I format the tests (input, expected output, bla bla.)?
>	- `It's ok how I thought about it`
>- Should I to put it on the board?
>	-  `no`

