---
tags: [Notebooks/Digilent]
title: "Course Notes 12.04.2022 \U0001F4F2"
created: '2022-04-12T13:36:29.081Z'
modified: '2022-04-23T15:47:59.063Z'
---

# Course Notes 12.04.2022 :calling:

- Git
- Embedded Introduction
- Zybo ZYNQ project versioned

## GIT cont'd
- digilent 
- clone si rezolvare conflicte
- submodule
- integrarea branch urilor

# Demo Proiect ZYNQ

## Vivado Project part
- regenerare a proiectului folosind fisier .tcl (Tools -> Run .tcl)
- partea de hardware a proiectului
  - un block design cu componente IP instantiate

## Vitis Project part (software)
- regenerate project using xsct console. & provided script
- proiect gata compilat

## Zybo Z7
> Hybrid Alu FPGA 
- evolutie a FPGA, implementeaza often used circuits in fixed blocks (CPU, periferice)

---
# Embedded System (sistem inglobat)
> Implement specific functions

- both hardware and software (not-mandatory)

e.g. electronic injection (cars)

- Advantages (cost -- , size --)
- could be made re-programmable (flexibility++)

Core: Microprocessor / Microcontroller
> Difference? uProcessor (unitate care executa instructiuni + ALU), uController (contine si periferice care extind feature-set-ul)

- must take care of the interfaces (digital - analog (conversii), ports, periferice, senzori);

- we want good cost but maximize the flexibility (trade-off)

---
Case Study: :
- the PWM implemented on the Basys3. Was it Embedded System?
  - it IS, but it has fixed functionality, is controlled by physical actuators (switches), it could be reprogrammable but it is not easy to reprogram
  - it doesn't have a software component
---
### Embedded computing system:
- CPU
- Instruction / Data Memory
- Peripherals (controller PWM legat la LED tri-color);

- others: CLOCK, RESET (to be deterministic), POWER (power supply)

### ZYNQ 7000
---
Components:
- ARM 2 cores (CPU, cache, On Chip Memory) 
- FPGA
- Peripherals
- predefined interfaces:
  - Processor -> Memory Controller, Central Interconnect (Routing to peripherals/FPGA)
  - Colors (BUSES - AXI cele mai multe, AHB, APB) 

- XADC (ADC) - can add analog sensors

### AXI (buses)
> Arhitectura de bus <Advanced Extensible Interface\>

- master-slave topolog - un port master e legat la un singur port slave. 
  - semnalele din interfata sunt uni-dimensionale
  - Interconnect component rezolva conexiunile point-to-point a.i. sa poti sa legi mai multi master cu mai multi slaves

- handshake mechanism = pentru a transfera date intre master si slave (Ready = 1 , Valid = 1, rising_edge(CLK))

- mai multe tipuri de AXI 
- AXI4 = memory-mapped, AXI4-Lite, AXI4-Stream (video apps)

## Accesarea Perifericelor
- adresarea se face prin maparea datelor (instructiuni, periferice) pe adrese.

- adresele ne permit sa facem READ/WRITE
- adrese <-> functionalitati
- ***Interconnect*** component implementeaza maparea (addresses decoder)

## Interconnect
- XBar
- Couplers (adaptare intre diferite tipuri de AXI buses)
- putem avea clocks diferite pentru masters and slaves

## Conexiune
- axgtio - FPGA part
- AXI Interconnect - GP Ports

## ZYNC project
- GOAL: controller de RGB LED (embedded pe placuta) pe placa ZYBO (ARM + FPGA Artix7)

  - No OS
  - OS
  - App pe linux 
  => Embedded System
## TODO:
- setup vitis project :white_check_mark:
- repo nume in vhdl club introdu numele in README.md :white_check_mark:
- Homework : Set up project :white_check_mark:
- Test project from the beginning :white_check_mark:

