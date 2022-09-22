---
tags: [Notebooks/CA]
title: Lab 8.0 MIPS Memory Unit + Write Back
created: '2022-04-07T12:26:56.341Z'
modified: '2022-04-08T11:49:38.486Z'
---

# Lab 8.0 MIPS Memory Unit + Write Back

## Memory Unit MIPS
Components: 
1. **Data Memory**
  - RAM with asynchronous read and synch write
  

|Inputs|Outputs|
|------|-------|
|ALURes (address)|ALURes|
|RD2 (data)|MemData (dout)|
|MemWrite | *means: control signal*|

2. **Write Back Unit**
- basically a MUX controlled by MemToReg signal


3. Other components
- AND for PCSrc :white_check_mark:

## TODO:
1. Design Memory Unit :white_check_mark:
    - validate MemWrite With an MPG signal
2. Add write back unit and jmp computation :white_check_mark:
    - wbu in a oneliner;
    - jump computation et. al.
3. Test everything 
  - most instructions :white_check_mark:
.
.

4. ***sw, lw - make sure they work*** :white_check_mark:
