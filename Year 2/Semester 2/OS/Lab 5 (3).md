---
tags: [Notebooks/OS]
title: Lab 5
created: '2022-03-17T10:31:37.267Z'
modified: '2022-03-20T07:38:26.987Z'
---

# Lab 5

- Same reading material as lab 4

## Tips regarding coding
- read operation is slow

## :pushpin: TODO:
- probleme guidance
- searching - important pentru assignment

## Assignment info :sunglasses:
*Read multiple times
- Header 
  - describes information placement
  - create a struct for parsing the format of the section
  - careful about alignment (i.e. fiecare tip de date o sa prefere sa fie la o anumita adresa de memorie, e.g. int -> multiplu de 4) --> 

- Body - stim un offset 

- What we gotta do

  - compilare fara erori
  - :warning: **IMPORTANT**: sa functioneze comanda de variant
  - outputul pentru comenzi trebuie sa arate exact ca in fisier
  - reuse the tasks_solutions for further solutions

- ***Command line argument parsing*** (fara librarii), can't assume the order of the arguments

  - Hint: ar fi bine sa nu folosim multe if-uri (a.k.a. hardcodam). E.g. use a for. 
  - Define error_messages and stuff, error_checking embedded in code;

### Alignment solution - ca sa nu ne batem capul
  ```
  #pragma pack(push, 1) //rezolva auto-aliniamentul
    
    struct...
  
  #pragma pop
  ```
