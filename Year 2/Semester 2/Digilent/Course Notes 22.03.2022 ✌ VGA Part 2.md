---
tags: [Notebooks/Digilent]
title: Course Notes 22.03.2022 ✌ VGA Part 2
created: '2022-03-22T08:07:49.763Z'
modified: '2022-04-23T15:47:08.405Z'
---

# Course Notes 22.03.2022 :v: VGA Part 2

## TODO:
- Olympic games logo - inlantuire!
- 
**Update on resolution stuff**: linked to timing analysis + frequency

## VHDL Libraries & Packages (14)
- in the Vivado installation directory
Type declarations
Function (addition, operations, conversions)
  - functions with the same *name* are overloaded (interpreted) depending on what parameters **careful to add the same return type**

Package Body
- contains the implementations of the supported functions.

**Useful** to see the matchigs between opperands and so.

- Packages portabile in orice mediu de programare
- Careful with std logic arith


## Triunghiuri Images
Vrem să desenăm un triunghi plin
- 3 edges
- stim coordonatele varfurilor => dreapta definita de 2 vf
- divide in 2 planes w.r.t. the line
$c_2, c_3:$
- description in pptx, make the image dynamic based on the sw + btn (move the selected corner with the udlr buttons)

- clk after prescale is 100Hz = 10ms

- use 3 flags to mark where we are on the screen w.r.t 

## Olympic Circles Examples
- more constants grouped in types
- for loop used

### ***High resolution - the image is corrupted***
- we send Hsync, Vsync, R, G, B
- sync should instruct monitor to move the pixel ray such way
- we don't send any clock to the monitor, but the monitor recreates its clock based on the synchronization signals we send
- it gets messed up because of the propagation delay => maybe use a register at the output (?)
- we will observe some time analysis tools offered by Vivado

## Timing Analysis
- the RGB is delays w.r.t sync signals
- we will consider the transfer between synchronized registers => N.E.A.T
$t_{int}+t_{reg}+t_{out}$
- backlash: CRITICAL WARNING - timing reqs not met

## TEMA
Triunghiul - desenez doar linile, ramane functia de miscat colturile
- grosime linie de vazut cum o rezolvam

<p align="center">
  <img src="@attachment/homework_1.jpg" width="1000">
</p>

---

### Idei tema
Pentru ca o linie de grosime width sa fie afisata, punctul de pe egran trebuie sa fie cuprins intre o dreapta exterioara si una interioara:

- External vertices: E1, E2, E2
- Internal vertices I1, I2, I3 - declared with respect to the outer ones :raising_hand:


>point on edge E1(I1) - E2(I2) => point is on the semiplane on the left of (E1,E2) and on the right of (I1,I2)

3 Flags - 1 for each edge

flg1 - point is that way between the 

flg2, flg3

