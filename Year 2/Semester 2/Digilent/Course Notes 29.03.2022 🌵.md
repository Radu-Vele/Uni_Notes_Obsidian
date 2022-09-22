---
tags: [Notebooks/Digilent]
title: "Course Notes 29.03.2022 \U0001F335"
created: '2022-03-29T13:12:01.935Z'
modified: '2022-04-05T13:47:33.462Z'
---

# Course Notes 29.03.2022 :cactus:

Solution to previous homework:
- will be uploaded later

## Timing analysis
- based on the Olympic circles project

### Timpii de propagare
---
- nu sunt niciodata 0 
- in interiorul vga: 
  frecvente mari -> distante mari (linii lungi)
- in Vivado - compute propagation time from flipflop to flipflop (ff use the same clock signal)
- remember how time delays impact a flip flop
- datele nu au voie sa se schimbe intre t_setup si t_hold w.r.t rising edge

### :white_check_mark: Rezolvarea problemei de timing:
- in combinatorul de imagine asteptam un semnal de la ckVideo pentru a atribui semnalele la pinii VGA (adaugam bistabile)
- vivado o sa ne genereze bistabile numai pentru bitii care o sa ajunga la un moment dat sa fie folositi :cool:

>compilatorul optimizeaza numarul de componente daca cumva refolosim date and stuff

=> Flip Flop Added => Design failed to reach the timing requirements

- the fact that the circuit is not ideal ( $time \ne 0$ ) is important in order for us to be able to implement projects

### The segments of the timing path:
---
### Intra Clock
### 1. Setup time
- ***Slack*** calculat w.r.t. more parameters

- Report timing summary - Vivado (IMPLEMENTATION), vedem care rute nu respecta timing requirements.
### 2. Data path
### 3. Destination clock path 

## Our mission: optimizarea operatiei din data path. :cop:
- incercam sa facem cai de date mai scurte
- **introducem bistabili**, rupem path urile
- we will increase the **latency** (the adress on the screen will be transmitted earlier) :worried: => maybe delay the addresses too (dar imaginea va ajunge mai tarziu cu un clock cycle pe ecran)
### Pipeline FlipFlop :sparkles:
- new problems after this addition of FFs (more paths where the slack value is out of bounds) => adaugam mai multe niveluri de pipeline flipflops (ar fi bine sa fie distribuiti pe path)
- 3 pipeline flipflops solve our issue

---
### Hold Analysis
- similar procedure, slack issues (that are not present in our design)

---
### Pulse-Width Analysis

---

### Excel file:
- analiza resurse, rapoarte de timp

## TODO:
- Answer: De ce e o diferenta asa mica de FF si LuT in cazul MinMin cand punem 3PLFF in loc de 2PLFF?

:white_check_mark: Hypothesis:
Registri extra (adaugati pentru varianta 3 PLFF) sunt absorbiti in DSP-uri (au pe intrare si iesire un rand de registri).

- Check teams channel for any other information
