---
tags: [Notebooks/Digilent]
title: "Course Notes 19.04.2022 \U0001F4BB"
created: '2022-04-19T13:29:47.483Z'
modified: '2022-04-23T15:47:23.442Z'
---

# Course Notes 19.04.2022 :computer:

## General Info
Lessons Learned Zybo Demo:
- proiectul poate fi modificat din soft at runtime.

Next week facem sedinta:
- for linux stuff.
- *if* we miss it we should watch recording and recover everything.

# Vivado GPIO Project cont'd.
What we have:
- hardware platform definition
  - why? because (unlike uControllers), FPGA is initially "blank".
- bitstream (info to FPGA)

## How to work with designing embedded systems on FPGA?
- separation of tasks based on the diagram
- Vivado implements all the steps
- IDE (Vivado -> ***project-mode*** -> .xpr project) vs Tcl (script)

Separation between hw (Vivado) and sw (Vitis)?
- Handoff: Export - Import

|Export - Import|What is it?|
|------|-|
|Bitstream|FPGA links|
|Processing System (Zynq-only)| configureaza procesorul|
|IP-s||


## Version Control
How to do it like FPGA companies?

What we version?
- .tcl script that re-generates project (using the checkout command)

> Minimum necessary (low storage) info (source files) about a project: .vhd, .xdc, .c, .h, .asm

- conflict management is difficult/impossible in byte code

- :star: Export hardware in a different commit
(Vivado -> Export) => archive with the definition of the hardware platform


## How to version our Project?
- mod de lucru in care fiecare avem branch ul nostru dedicat.
- rulam checkin.tcl => fisiere .tcl pentru versionare
- nu avem xdc in proiect pentru ca folosim block automation => board

## Adding ILA
- debug purposes

# Vitis - software part
### About Vitis
- previously called SDK
- Workspace = project
- we need to control UART controller (Detalii in platform details)
- we can debug as well
- acum noi lucram intr-un mediu standalone (no OS)
- Bootloader = incarca o aplicatie pe zynq
### Zynq
- GPIO registers
- We are accessing the physical memory directly (addresses)
```
Register_Address = IP_Base_Address + Address_Space_Offset
```
### What to access?
1. LEDs
2. Buttons
3. Switches

Through the Data and 3-State Registers :white_check_mark:

---
### How running a program works?
Run (helloWorld.c in debug) -> (core, elf, debug options):
- reset system
- program ps
- run ps7_init (Configure registers)
- run post_config 
- download .elf in memory

aand it's on

### Turning on a LED
- linked to GPIO1
- configure the 3-state register bits as output (0)
- write the 4 bits in DATA register with the desired output

---

## TODO:
- checkout the mapping to leds (19:00 ish) :white_check_mark:
- change commit name to include the hash of the place where we got the export :white_check_mark:
- study ZYNQ aspects + Embedded

- tema : modify hello world app such that it will modify the leds (use direct and physical addressing) :white_check_mark:

```C
*(u32)(0x41200000) = ... ; //pointer to memory gets a value
```
- citirea switch-urilor si integrarea lor cu led-uri (afisam pe led-uri ce punem pe switch-uri). - in C. :white_check_mark:
