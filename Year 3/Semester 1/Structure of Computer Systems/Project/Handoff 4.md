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

> [!warning] Previous design mistake
> The mux added at input B of ALU in EX stage should be placed before the one that switched between I type or R type
> `TODO: modify the diagram in the documentation :)`

- [x] the hazard occured

Implement hazard detection unit

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


