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
	- [x] Done

### Test all supported instruction
R-Type
- [x] Done
I-Type (addi subi)
- [x] Done
Load
- [x]  Done
Store
- [x]  Done
Branch
- [x]  Done
Jump
- [x]  Done

---

## Implement Hazard Detection Logic:

### 1. EX Forwarding unit
- [ ] Tested functional
- [ ] TopLevel functional

### 2. MEM Forwarding unit
- [ ] Tested functional
- [ ] TopLevel functional

### 3. HDU ID
- [ ] Tested functional
- [ ] TopLevel functional

### 4. Add branch to ID stage
- add jump computation in IF `necessary? - I guess yea`

#### 4.1. Extend HDU
- [ ] Tested functional
- [ ] TopLevel functional

#### 4.2. Forwarding Unit ID
- [ ] Tested functional
- [ ] TopLevel functional


### 5. BHT Implementation
- [ ] Tested functional
- [ ] TopLevel functional


