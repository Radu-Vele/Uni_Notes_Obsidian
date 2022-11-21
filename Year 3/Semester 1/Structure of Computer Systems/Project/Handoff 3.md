# Design 🎨

## Indications
- Actually start the job

- Do the design of each component - and maybe implementation of them, or low level design + beginning of implementation

- Finally do the whole design

## To do
### a. Forwarding Unit
- [x] Done
- add schematics
	- [x] fwd exe
	- [x] fwd mem
	- [x] initial mips (not done by myself) - pdf
- explain the decisions to be checked and the meaning of the outcome (MUX)
	- [x] Done

- make sure to check when a store depends on the previous instruction
	- [x] Done


### b. Load Data Hazard (Hazard Detection Unit)
- [x] Done


### c. Branch Control Unit
- move branch decision to ID stage

> [!warning] We may need data forwarding in ID for comparing the registers.
> -  extend functionality of the hazard prediction unit to determine if we have a branch and the previous instruction adds a dependency 
> - add a forwarding unit for the RF outputs (where equality comparison is performed) to bring 

- [x] Done
- mechanism for flushing
	- [x] Done
- branch history table implementation
- https://www.youtube.com/watch?v=-T8yDJ8vTuI useful
	- [ ] Done

### Add MIPS supported instructions
 - [x] Done



# Delivery

> [!question] Questions
> - do I need to be able to branch to a lower address (How)? - my bht doesn't make sense if I don't have loops `I should`
> 	- implications - branch address can be computed with a adder-subtractor, control the PC so it doesn't go nuts I guess `yep`
> 	- jump address computation in IF? `yes, I should`
> - is it ok on 16 or 32 bits? `16 is fine`
> - Is my control logic for branch alright? 

