# Implementation 1 👨‍💻
- write some code
- be able to test it and show - no grade though
- should finish implementation by `19 December` - ask documentation questions before that

## Add testbenche for individual components
> [!question] Questions?
> - should I make testbenches for each forwarding unit/hazard detection?
> 	- `I guess so`
> - mips testbench for Identifying the instructions more easily? - set some aliases maybe? `not really necessary`

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

```
-- R-type instructions program
--         B"000_001_010_100_0_001", -- add 1 = 1 + 2
--         B"000_001_010_100_0_010", -- sub 4 = 1 - 2
--         B"000_001_010_100_1_011", -- sll 4 = 1 sll 1
--         B"000_001_010_100_1_100", -- srl 4 = 1 srl 1
--         B"000_001_010_100_0_101", -- and 4 = 1 and 2
--         B"000_001_010_100_0_110", -- or 4 = 1 or 2
--         B"000_001_010_100_0_111", -- xor 4 = 1 or 2
-- I-Type instructions
--         B"001_001_100_0001010", -- addi add 4 = 1 + "A" (D)
--         B"101_001_100_0000010", -- subi sub 4 = 1 - "2" (1)
-- Load and Store
--         B"010_001_101_0000001", -- load lw  5 = MEM(1 + "1") (abc8)
--         B"011_001_101_0000010", -- store sw MEM(1 + "2") = 5 HAZARD -- info ready after 4 clock cycles
--         B"011_001_100_0000011", -- store sw MEM(1 + "3") = 4
-- Branch Not Taken and Taken
--         B"100_001_010_0000100", -- branch on equal 1 2 
--         B"100_011_100_1111110", -- branch on equal 6 7
-- Jump
--         B"111_0000000000100", -- jump to address 4
```

---

## Implement Hazard Detection Logic:

### 1. EX Forwarding unit
- hazard occurence is confirmed on simulation

```vhdl
 B"000_001_010_101_0_001", -- I1 $5 = $1 + $2 -- no dependency
 B"000_001_010_100_0_001", -- I2 $4 = $1 + $2 -- no dependency
 B"000_100_010_100_0_001", -- I3 $4 = $4 + $2 -- Depends on I2 => Forward from previous to ALU Input A
 B"000_101_100_011_0_001", -- I4 $3 = $5 + $4 -- Depends on I1, I3, I2 => Forward from previous to ALU Input B
```

Changes:
- send over the ID/EX pipeline the RS and RT addresses
	- [x] Done
- implement read after write in register file - `a bit trickier` 

>[!important] Solution
>	write on rising edge read on falling edge	
- [x] Done

- condition for detection
```vhdl
Forward_A <= "00";
Forward_B <= "00";

-- less priority
if MEM_WB(35) = '1' then -- MEM_WB_RegWrite = 1
	if MEM_WB(34 downto 32) = ID_EX(88 downto 86) then -- MEM_WB_RegDest == ID_Ex_Rs
		Forward_A <= "10";
	elsif MEM_WB(34 downto 32) = ID_EX(85 downto 83) then -- MEM_WB_RegDest == ID_EX_Rt
		Forward_B <= "10";
end if;

-- more priority
if EX_MEM(55) = '1' then -- EX_MEM_RegWrite = 1
	if EX_MEM(2 downto 0) = ID_EX(88 downto 86) then -- MEM_WB_RegDest == ID_Ex_Rs
		Forward_A <= "01";
	elsif EX_MEM(2 downto 0) = ID_EX(85 downto 83) then -- MEM_WB_RegDest == ID_EX_Rt
		Forward_B <= "01";	
end if;
```


- [x] Tested functional
- [x] component functional

- [x] TopLevel functional

### 2. MEM Forwarding unit
- a store (data to be written) depends on the previous instruction or on the instruction before the previous one

Changes in hardware:
- add a WB buffer to check the dependency to the instruction before the previous one

> [!important] Solved Previous design mistake
> The mux added at input B of ALU in EX stage should be placed before the one that switched between I type or R type
> `TODO: modify the diagram in the documentation :)`

- [x] the hazard occured

```vhdl
Forward_C <= "00";

-- less priority
if WB_BUF_RegWrite = '1' then -- MEM_WB_RegWrite = 1
	if EX_MEM_Rt = WB_BUF_RegDst and EX_MEM_MemWrite then
		Forward_C <= "10";
end if;

-- more priority
if MEM_WB_RegWrite = '1' then -- MEM_WB_RegWrite = 1
	if EX_MEM_Rt = MEM_WB_RegDst and EX_MEM_MemWrite then
		Forward_C <= "01";
end if;
```

- [x] Tested functional
- [x] component functional

- [x] TopLevel functional

```vhdl
-- Data Hazard RAW in EX stage
      B"000_001_011_011_0_001", -- add $3 = $1 + $3 -- no dependency
      B"000_001_010_011_0_001", -- add $3 = $1 + $2 -- no dependency
      B"011_011_011_0000001", -- store MEM($3 + '1') = $3 -- depends on the previous two (but latest is taken into account)
      B"011_011_011_0000010", -- store MEM($3 + '2') = $3 -- depends on the i. before the previous one
      B"011_011_011_0000011", -- store MEM($3 + '3') = $3 -- no dependency
      others => x"0000"
    );
    
```

### 3. HDU ID

- confirm hazzard occurrence
	- [x] Done
- added necessary hw configurations
	- mux for ctl signals
	- pc en
	- if_id enable
- Did not create tb for this component!

> [!important] `Solved` Stalling works but
> - the forwarded data to the register that comes from the mem unit is the ALUOutput, not the memory output
> - Solution `forward the result of the WB MUX, not the ALUOut pipeline value from MEM/WB`

- [x] Tested functional
- [x] TopLevel functional

```vhdl
-- Load Data Hazard
      B"010_001_011_0000001",-- load $3 <= MEM($1 + '1')
      B"000_011_100_010_0_001",-- add $2 <= $3 + $4
      others => x"0000"

-- Load Data Hazard
      B"000_011_100_001_0_001",-- add $1 <= $3 + $4
      B"000_011_100_010_0_001",-- add $2 <= $3 + $4
      B"000_011_100_101_0_001",-- add $5 <= $3 + $4
      B"000_011_100_110_0_001",-- add $6 <= $3 + $4
      B"000_011_100_111_0_001",-- add $7 <= $3 + $4
      B"100_001_010_1111011", -- beq 1 2 -5
      B"000_011_100_000_0_001",-- add $0 <= $3 + $4
      B"000_000_011_111_0_001",-- add $7 <= $3 + $0

      others => x"0000"
```

> [!important] Documentation modification  📝
> - we don't forward from ALUOut in MEM/WB, but from WB_MUX_Out
	
### 4. Handle control hazards

#### 4.0 Move branch to ID stage
- add comparison unit to ID
	- [x] Test with no other hazard - looks promising
	- [x] Detected the hazard (next instruction's impact is visible even though we jumped)

- remove branch from MEM and EX units 
	- [x] Done
- remove zero detection from ALU

> [!remark] Finally
> I will remove the unused signals from the pipeline registers - error prone big time

#### 4.1. Add flushing mechanism
- mechanism: basically reset the IF/ID i.g and set all control signals to 0
-  [x] Tested functional

#### 4.2 BHT Implementation
- [x] Tested functional in IF unit
	- [x] it looks pretty good, now I just need some test cases in the toplevel to make sure they are covered

> [!important] `Solved:` Issue with data hazards resolution
> - check why XXXX value is forwarded to ALU inputs
> - ![[Pasted image 20221212224814.png]]
> - solution: `added the condition to check forward the reg file write data to read data only when the regwrite signal is on HIGH`

- fibonnaci code tested ok - after two iterations, the right target address is chosen
	- [x] Done

```vhdl
    -- infinite fibonnaci
      B"000_001_010_011_0_001", -- 0: add $3 = $1 + $2
      B"000_010_000_001_0_001", -- 1: add $1 = $2 + $0
      B"000_011_000_010_0_001", -- 2: add $2  = $3 + $0
      B"100_000_000_1111100", -- 3: beq $0 $0 -4
      B"000_001_010_011_0_001", 
```

- check some more situations
	- branch is not taken anymore (loop is finished)

>[!important] `Solved:` I kinda need bneq for looping with a purpose
>- what does it imply to add branch on not equal?
>	1. Modify the branch taken signal in ID to be 
>		`Branch_Taken <= '1' when ((temp_rd1 = temp_rd2 and Branch_instruction = '1') or (temp_rd1 /= temp_rd2 and Branch_NE_instruction)) else '0';`
>	2. branch address is the same
>	3. Add to control unit the case for branch not equal and generate the signal (no need for propagation)

- add bnq
	- [x] Done
- test
```vhdl
-- Dynamic branch prediction
    -- 5 fibonnaci numbers to be computed 2 -> 5 -> 7 -> 12 -> 19
      B"011_000_000_0000000",-- 0: store MEM[0] <= $0 - constant 0
      B"010_000_100_0000000",-- 1: load $4 MEM[0] = 0
      B"010_000_101_0000001",-- 2: load $5 MEM[1] = 5
      B"001_100_100_0000001", -- 3: addi $4 = $4 + 1 -- counter
      B"000_001_010_011_0_001", -- 4: add $3 = $1 + $2
      B"000_010_000_001_0_001", -- 5: add $1 = $2 + $0
      B"000_011_000_010_0_001", -- 6: add $2  = $3 + $0
      B"110_100_101_1111011", -- 7: bneq $4 $5 -5
      B"011_000_010_0000110", -- 8: store MEM[6] <- $2
      others => x"0000"
```
- [x] Does NOT work properly

> [!important] `Solved` Design Issue
> - In the BHT mechanism, if a branch was taken and it was not supposed to be taken, the flush signal selects the multiplexer that loads the branch address to PC, but we want the `Previous!` PC + 1 address to be loaded in that case (MSB_Pred = 1 and )

> [!important] `Solved`Synchronization issue
> - branch taken signal needs to be generated only after the registers have been read (falling edge clock)
> - at the moment the branch taken signal is not generated properly
> - there is actually no need for this!!!

- [x] The moment a loop is exited works ok
- [x] Make sure it iterates the right number of times

```vhdl
-- Dynamic branch prediction
    -- 5 fibonnaci numbers to be computed 2 -> 5 -> 7 -> 12 -> 19
      B"011_000_000_0000000",-- 0: store MEM[0] <= $0 - constant 0
      B"010_000_100_0000000",-- 1: load $4 MEM[0] = 0
      B"010_000_101_0000001",-- 2: load $5 MEM[1] = 5
      B"001_100_100_0000001", -- 3: addi $4 = $4 + 1 -- counter
      B"000_001_010_011_0_001", -- 4: add $3 = $1 + $2
      B"000_010_000_001_0_001", -- 5: add $1 = $2 + $0
      B"000_011_000_010_0_001", -- 6: add $2  = $3 + $0
      B"110_100_101_1111011", -- 7: bneq $4 $5 -5
      B"011_000_010_0000110", -- 8: store MEM[6] <- $2
      B"111_0000000000000",-- 9: Jump 0
```

- execute the same program multiple times
	- Add a jump to the beginning!
	- [x] Works properly (BHT allows us to loop correctly straight from the first iteration)

- [x] TopLevel functional

#### 4.2. Extend HDU (no loads before branch)

- possibility:
	1. previous instruction (R or I type) had the destination address equal to one of the sources of the branch 
```vhdl
B"000_001_010_011_0_001",-- add $1 $ 2 $3
B"100_001_011_0000010", -- beq $1 $3 
-- exprected behavior: branch is taken even tho it was not supposed to
-- the condition ID_Branch = 1 and ID/EX RegWrite = 1 and source of branch equals destination of ID_EX
```

- [x] Test Occurance of the conditions
	- the conditions occur (may need to be careful if I impact the branch taken signal generation :/ - I don't want to impact the BHT or so)

Add stalling for the prv instruction
- [x] Done
Tested ok
- [x] Done

- [x] Tested functional
- [x] TopLevel functional

#### 4.3. Forwarding Unit ID (no loads before branch)

- added the forwarding unit in ID

```vhdl
    -- branch after write condition
      B"000_001_010_011_0_001",-- add $1 $ 2 $3
      B"100_001_011_0000010", -- beq $1 $3 
      B"000_101_110_111_0_001", -- add $5 $6 $7
      others => x"0000"
-- with forwarding the branch is taken as initially 1 is equal to 3 but the addition on instruction 0 changes the value of 3
```

- [x] Tested functional
- [x] TopLevel functional

Does it work for the case when I initially dont take the branch, but then I do
- [x] Yep

#### 4.4. ID FWD from inst before the previous
- need to insert a stall if there is a dependency between current branch in id and the instructions 2 steps before (EX/MEM)
- but **no forwarding** is required

```vhdl
    -- branch after someting after write condition
      B"000_001_010_011_0_001",-- add $1 $ 2 $3
      B"000_101_110_111_0_001", -- add $1 $2 $3
      B"100_001_011_0000010", -- beq $1 $3 
      B"000_101_110_111_0_001", -- add $5 $6 $7
      others => x"0000"
```

check the condition
```vhdl
EX_MEM_RegWrite = '1' and ID_Branch = '1' and EX_MEM_RegWrite = ID_Rs or ID_Rt
```


Does it work for the case when I initially  take the branch, but then I do not?
- [x] Yep

#### Special case for load before branch: check
- 2 stalls are inserted
```vhdl
-- branch after write condition
    B"010_000_011_0000000", -- load $3 = MEM[0]
    B"100_100_011_0000010", -- beq $4 $3 
    B"000_101_110_111_0_001", -- add $5 $6 $7
```

#### Check what happens to the BHT in the context of stalling the ID for branches
- not really sure, I could leave this for the testing part, maybe add an enable that works at the same time with pc enable (for writing) - it looks pretty much alright

- add jump computation in IF `necessary? - I guess yea
	This should not really raise any issues regarding other components
	- [x] Done

🏆


