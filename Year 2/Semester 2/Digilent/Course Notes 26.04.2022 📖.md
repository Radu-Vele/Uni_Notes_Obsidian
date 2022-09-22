---
tags: [Notebooks/Digilent]
title: "Course Notes 26.04.2022 \U0001F4D6"
created: '2022-04-26T13:30:09.586Z'
modified: '2022-05-01T10:07:57.675Z'
---

# Course Notes 26.04.2022 :book:

## Homework Feedback
- careful about versioning (make sure that gitignore works well, compare with elodg/main branch)
- we can check ILA if the board is programmed

## Follow-up Vitis

### Accesare registri:
- use xgpio.h library - gpio driver + other headers generated in bsp
- constants predefined are being used 
- buttons are added to invert the leds display (elodg example)

## Our project RGB pwm LED controller
- we use the pwm controller designed with GaborCs
- we want to make our own custom IP

### Custom IP:
- we will need to implement a few registers for the software support
  - 8 - bit registers (duty factor, clk divider, control)

- we also need an interface AXI
  - use AXI Lite (proper latency, easy to implement)

- use a wizard
- no bitstream is needed, only synthesis (BUT synthesis is aimed on the board specified in the origin design - won't change for zynq as it is the same for 7-series)

## Further steps:
Vivado
- include 3 PWM IPs into the block design of the hardware platform (pwm_ctrl_red/green/blue)
- add constraints for zybo
- version the hardware platform
- export hardware

Vitis

- update the hardware platform
- write a driver for the pwm (.c file with basic functions)
- include modify the .c code such that we will obtain a white LED
- version the project
.
.
.

## TODO:
1. Get up to date by rewatching :white_check_mark:

    - figure out the git issue with the proj/simple-gpio :white_check_mark:
 
2. Finish PWM project :white_check_mark:

    - folosim 3 canale pentru PWM controller (pwm) (explained in video) sau multiplicam IP-ul (3 ip-uri la fel R G B)

3. Upload on GitHub all the recovered stuff :white_check_mark:

4. Homework: Implement - o trecere intre culori dintr-una in alta si sa se repete-  :white_check_mark:
    - controlam fiecare componenta de culoare independent si la viteze diferite

## Wrap-up Embedded System Standalone 
1. Git
- basic functionality and how to use
2. Vivado and Vitis versioning
- Digilent way
3. Scripting (tcl)
4. Develop on one's own branch
5. Basic helloWorld project
6. Controller PWM RGB Led
    - and the software component
    - drivers
    - custom IP & driver

## Next time:
OS Built on the hardware platform
- extending the RGB LED project

Instructiuni pe teams
- folosim o masina virtuala (detalii pe teams) :white_check_mark:
- card microSD formatat

