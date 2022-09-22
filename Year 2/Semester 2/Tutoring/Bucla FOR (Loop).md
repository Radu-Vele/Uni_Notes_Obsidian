---
tags: [Notebooks/Tutoring]
title: Bucla FOR (Loop)
created: '2022-03-24T18:11:43.856Z'
modified: '2022-04-08T09:12:50.595Z'
---

# Bucla FOR (Loop)
## I. Introducere

De ce folosim for loop? - vrem ca o secvență de cod să fie executată de un anumit număr de ori.

### - Sintaxă:

```C
int i;
for(i = 0; i < max_1; i++) {
  //instructiuni
}
```
> Explicatie:
---> for ( <initializare (de la cat incepe i)\> ; <limita superioara\>; <incrementare\>) 
------> i++ înseamnă i = i + 1, adică **incrementare**;

> i = (denumire) **iterator**

## II. Exemple de cod
### (*) Initializare a unui tablou folosind "for"
```C
int i;
int nr_elemente = 20 //ai putea sa il citesti de la tastatura
int tablou[nr_elemente]
for(i = 0; i < nr_elemente; i++) {
  tablou[i] = i;
}
//rezulta un tablou care are valoarea elementelor egale cu indexul
// valoare | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |
// -------------------------------------------------------------------------------------------------
// index   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |
```

### (*) Afisare a continutului unui tablou
```C
for(i = 0; i < nr_elemente; i++) {
  printf("%d", tablou[i]);
}
```

## III. Exerciții

### 1. Scrie un program care construiește un tablou în care valoarea la indexul curent este egală cu pătratul indexului. Apoi, afișați conținutul tabloului.
>Exemplu:
pentru tablou[3] valoarea va fi pow(3, 2) = 9;

### 2. Scrie un program care găsește cel mai mare și cel mai mic element dintr-un tablou și le afișează. Mărimea tabloului va fi citiă de la tastatură.
> Hint: poți să folosești codul de mai jos pentru inițializarea tabloului.

```C
int nr_elemente;

//aici scrii linia de cod care citeste de la tastatura numarul de elemente

int tablou[nr_elemente];

for(int i = 0; i < nr_elemente; i++) {
  if(i % 2 == 0) {
    tablou[i] = nr_elemente - i;
  }
  else {
    tablou[i] = i;
  }
}

//aici vine codul tau care calculeaza minimul si maximul + afisarea
```

## IV. Resurse
- https://www.geeksforgeeks.org/loops-in-c-and-cpp/#:~:text=A%20for%20loop%20is%20a,steps%20together%20in%20one%20line.&text=In%20for%20loop%2C%20a%20loop,used%20to%20control%20the%20loop. [ Explicatie Geeks for Geeks + Diagrame bune]

- https://www.youtube.com/watch?v=Qn8dNgvqPoo [Explicatie video]

- https://ro.education-wiki.com/9257635-for-loop-in-c [Explicatii în lb.română]



