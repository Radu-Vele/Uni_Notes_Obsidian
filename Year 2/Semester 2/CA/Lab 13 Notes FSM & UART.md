---
tags: [Notebooks/CA]
title: Lab 13 Notes FSM & UART
created: '2022-05-20T11:10:35.189Z'
modified: '2022-05-20T11:25:07.423Z'
---

# Lab 13 Notes FSM & UART

# Communication protocols Basys supported

## I2C
- synchronous
- 2 signals (clk, serial data)

## STI
- serial interface
- 4 signals (clk, chip selecet, MOutput, MInput)

# Our focus : UART
- we need info about the start & end of message
UART Packet:
1. Start bit
2. End bit

$baud\_rate = bits/sec$

## FSM 
- transition between stated w.r.t. certain signals
- communication board -> terminal emulator

## TODO:
- new project -> test env
- implement the TX_FSM entity + FSM implementation (Appendix 7) -> set outputs in each state


- baud rate: 9600
  - 9600 Hz is what we need (1/s = Hz);
  - we have 100MHz we need to divide by 10416;
  - in test_env we will need to use BAUD_EN based on a counter to 10416;
