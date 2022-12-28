# First Order Logic cont'd

## Assignment 

> [!info] Assignment on Logics
> - Deadline `Sunday 18 december`
> - Postponed for `23 december`

**Task**: Implement something of your own choice with Prover9/Mace4.

Deliverable:
1.  source code in zip format
2.  documentation using the laboratory template

**Evaluation**:
Main criteria: originality, creativity.
Other criteria: code quantity in Prover9/Mace4/Python.

### Ideas: 

1. MineFOL + Pacman. Pacman gets messages in FOL where the food is.

---

# Lab 8 Material - Inference in FOL

### Resolution
### Skolemization
- implement the who-killed-the-cat problem
### Paramodulation
- deal with equality in mace4
### Demodulation
### Wumpus



# Pacman MineFOL 🎮
### What it takes:
- have a matrix that contains the state of the positions in the matrix (U / S / NS)
- hardcode some messages in certain positions in the matrix
- everytime pacman hits a message, it calls prover9 to update the states of the safety mstrix
- can use the implementation of MineFOL from moodle

## Steps
- define problem:

> [!important] Problem definition
> > Pacman has to search for messages until all the mines are discovered (e.g. 4 mines). His path is shown at the end of the algorithm.
> 
> Details:
> - pacman always searches for messages (using any search algorithm)
> - he can only pass through positions that are proven safe
> - everytime he finds a message he calls mace4 to update the safety matrix
> - after one message is found, they search for another one
> - when the number of mines is discovered (a.k.a. the safety matrix contains as many 1s as the number of mines) the game stops

### Mace4 from Python
- run in mace4 for small puzzle
	- [x] Done
- format mace4 .in file from python
	- [x] Done
- run mace4 from python (call a shell script using `subprocess` module)
	- [x] Done
- read and parse out file from mace4 from python
	- [x] Done
- interpret format of the file 
	- [x] Done

Added files:
- `mace4Call.sh`
- `mace4_handle.py`

## Pacman stuff
- define problem
	- actually, **AStarSearchAgent does exactly this job** (I just don't have the heuristic) - employs the astar search algorithm i wrote
		- the search is only done once

> [!question] Questions?
> - how to add the safetyMatrix to the Agent?
> 	- `add it to its state`
> - how to check if the position is safe
> 	- `add only the successors we know are safe`
> - how to find out when a food item was found?
> 	- `the agent contains a matrix that has a T value where there is food`
> 	- `functions regarding that matrix (count nr of foods, etc.) are defined in game.py, there also are functions that change the values of the grid` (a.k.a. food was found)
> 	- check how the safety matrix and messages are transmitted such that a solution is found

### Solve for small input
- [x] Done

---

## Documentation
- add problem description
- explain
- add code snippets
- [x] Done

---

## Back to PacMan

### Try bigger problems
- find description of a bigger problem in FOL
- generalize all code
	- insert messages in messages.txt
	- insert initial formulas in initialFormulas.txt
	- for tiny maze add bfs for bigger add a*
	- [x] Done
- make it work
	- [x] Done
- add mineFOL from website

> [!important] Some weird stuff is happening
> - more models with the same values are generated
> - the count function gets 5 matrices

- MineFOL in prover9 understanding

## Back to documentation:
- include final code + explanations
	- [x] Done
- all add test cases
	- [x] Tiny FOL
	- [x] Small FOL