---
tags: [Notebooks/Digilent]
title: "Course Notes 24.05.2022 \U0001F4BE"
created: '2022-05-24T12:18:53.087Z'
modified: '2022-05-24T15:59:24.009Z'
---

# Course Notes 24.05.2022 :floppy_disk:

  
## Homework feedback
- read is slow that's why it crashes
- can use the driver for leds
- checkout Sopte's github

# UIO
- creates a driver in user space
- create a mapping such that a written program (to access IP) accesses memory safely (no overflow).

- accesul la memorie pentru un element hard care are asociat un driver e restrictionat pentru alte drivere

- we can only control pwm through devmem at the moment


## Disadvantages

- peripheral connected to UIO (instead of kernel)

- multiple peripherals having uio => uio1/2/3...10

- we initially don't have info about what uio is linked to.

### Interrupts
- we need interrupts in an embedded system
- UIO doesn't have the best interrupt handler
- we should avoid UIO interrupts
- worst thing: we are in user-space (context-switching).

Solutio: Zero-Copy
- user space --> kernel space (copy in kernel space) and reversed
- use some internal buffers


### Why useful though?

- prototype drivers without writing to kernel space
- testing & debugging

- libuio.c code on github/Digilent

# Control PWM led through UIO

## New Platform

## New Application

## Add comments to sources given with UIO functions

- add main.c to create pwm application


## Announcements:
- Digilent has more domains
- internship offers to be sent for some of the peeps
- other internship positions: analog electronics, junior webDev
- after insernship - possible 
- until thursday invitation: paid internship 

- give back hardware (until the end of the exam session).

Teams/Mail - to receive everything 


