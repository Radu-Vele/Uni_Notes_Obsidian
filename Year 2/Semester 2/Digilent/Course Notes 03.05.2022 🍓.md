---
tags: [Notebooks/Digilent]
title: "Course Notes 03.05.2022 \U0001F353"
created: '2022-05-03T13:14:39.203Z'
modified: '2022-05-10T13:35:27.716Z'
---

# Course Notes 03.05.2022 :strawberry:

## Homework Feedback:
- could make multiple loops (for each colors);

## Theory Intro

## Petalinux
> Nu e o distributie de linux, ci un wrapper over something
- folosim vrem sa scriem cod pentru a folosi GPIO dar sa rulam aplicatii din linux.

## Recap : Bare-metal (aka Standalone) -what we've done so far
- no virtual memory 

> Virtual Memory - a "cage" where the running process is locked so that the process can only access adresses within it. -> The kernel creates the virtual memory and manages the mapping between it and physical memory.

- app specific i.e. it can only do what has been designed to

- direct DDR memory: 1 to 1 Mapping (Double Data Rate Synchronous RAM)

- single thread (if we would make a multi-core app we would need to manually manage)

## OS (Linux) :star:

- can have multitasking, multiple threads (using)

- drivers help us (for example there are generic drivers that work for many devices, e.g. ethernet standard drivers)

- memory management is automated (Direct Memory Access) 

  - scatter-gather = send requests to multiple targets and aggregate repsponds

- avem deja stack uri USB, TCP/IP scrise (nu avem coliziuni datorita memory managementului automatizat)

|||
|-|-|
|User Space| Kernel Space|
|less permsissions - i.e. apps|hardware management - more dangerous|
|more protection|not accessible for modifying protocols and stuff|

- pagefile / swap 
  - ca un cache memory - diferita de DDR

## Booting
### ZSBL = zero stage boot loader (hardcodat in ZYNQ)
- se uita pe mediile de stocare (JTAG, SD, QSPI memory) 
- cauta FSBL -> il incarca pe on chip Memory

### FSBL = first stage boot loader
- fisier .elf
  - configure ZYNQ
  - write bitstream
  - load uboot

### SSBL = Uboot = second stage boot loader
- un bit file in FSBL

- SSBL - Uboot (deja un mediu de dezvoltare)

> Uboot un bare metal program super complex => Loads Kernel + are acces la drivere

- are access la USB, ethernet devices

- poti boota linux-ul din retea tftp prin uboot

- reads device tree and passes the control to the Kernel (loads kernel)

### Kernel

> Manages hardware and adds abstraction for the user, adds virtualization, scheduling, process management

- wrapped in fit image
- loads drivers (used by the user to access components) 

### rootFS
- file system din care rulam aplicatii and so.

### Terminal Print at booting
- incarcare a driverelor din zynq (+ base address)
  - e.g. GPIO (se afla in FPGA) 

### Pushing to git
- there is a gitignore file already

## TO DO:
- Read more about virtual memory
- Finish Build :white_check_mark:


## Questions
### What's the deal with ***virtual memory***?  

What is it helpful for?
+ Allocate different memory space for different processes (use *relative addressing*)
+ protection against overwrites (no access outside its address space)'
+ can introduce access right for different memory spaces
+ "The current running program *thinks* it s the only program running"
    - App wants to access mem => virtual address is sent to MMU (mem manag. unit) => maps virtual address to physical address of DDR (blocks may be mapped in different places - split - no fragmentation)

+ MMU organization -> there is some sort of LuT
  - Physical mem is divided into 4k ***Pages*** so that the nr of entries in LuT is lowered (there also is a Page Table)
  - There is a computation formula based on Page Address + Offset.
  - A cache is used (TLB - Translation Lookaside Buffer) to avoid accessing  the RAM every time to find an address
  
  - Memory swapping: release RAM space by temporarly storing information to hard drive
---
### De ce nu vede terminalul mesaje din FSBL in procesul?

A1: platforma nu este configurata pentru a avea abilitatea de a transmite mesaje / FSBL creeaza mediul in care se boot-eaza treaba. -- nope

A2: Anumite flag-uri din Vitis nu sunt enabled ca sa ne lase sa vedem mesaje

```
FSBL_DEBUG_INFO - to add to Vitis
```

---
- MyQuestion: Uninitiallized urandom is that ok?
