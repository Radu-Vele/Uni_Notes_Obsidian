# Implementation 👨‍💻
- write some code
- be able to test it and show - no grade though
- should finish implementation by `19 December` - ask documentation questions before that

## Add testbenche for individual components
> [!question] Questions?
> - should I make testbenches for each forwarding unit/hazard detection?
> 	- `I guess so`
> - mips testbench for Identifying the instructions more easily? - set some aliases maybe?

## 1. Test the existing pipeline:
- adapt it - define exact requirements
	- remove functionality for the branch on less than 0 and load upper immediate 
	- [x]  Done
	- remove sra, add MemRead functionality

- Test all supported instruction
	- R
	- [x] Done
	- make sure to cover the side effects (when control signals are 0, bla bla)
	- I

### Changes to pipeline:
1. Add branch to previous instruction
2. Add testbenches
3. Add hazard solution components

- testbench
	- [ ] Done
- Vivado simulation
	- [ ] Done
