# Analysis 

First, put thoughts in order and in **project proposal** write a list of features that we will meet.
- project proposal (all promised features)
	- [x] Done 
- project plan (divide our work)
	- [x] Done
- analysis - not sure about completeness
	- [x] Done

---

Test the existing pipeline:
- testbench
	- [ ] Done
- Vivado simulation
	- [ ] Done

---

## Analysis section
- elaborate the bibliographic research by discussing the implementation, include pipeline diagrams
- maybe flowcharts and **algorithms** (in my case the logic behind the Dynamic Branch Prediction)
- pipeline diagrams
- describe state machines (control states)

> [!Question] Questions
> Should I elaborate how every component is influenced? e.g. which registers are reset, or more examples?
> `...`
> Should I elaborate the design components?
> `...`
> Should I use something specific for algorithm? Pick existing procedure or make something myself?
> `...`
> Should I keep the planning part in the final documentation?
> `...`
> Would It be ok to start with a simple BHT and extend if needed?
> `...`

## Which branch prediction to choose?
[Source] Course CA 2nd Year

### Options:

FSM Predictors:
- state machines that register the likelihood of a branch

Bimodal - ⛏
- keep a counter for each branch instruction in the BHT
- based on the value in the counter we take / not that branch

Branch Target Buffer
- cache that determines the next address based on history
- for non-branches it shouldn't be a problem, as the memorized address is the next one

![[Pasted image 20221107082719.png]]
