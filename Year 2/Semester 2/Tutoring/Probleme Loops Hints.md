---
tags: [Notebooks/Tutoring]
title: Probleme Loops Hints
created: '2022-04-09T07:25:22.912Z'
modified: '2022-04-09T13:41:46.210Z'
---

# Probleme Loops Hints
## Bucla `WHILE`

>  DO-WHILE = ce e specific legat de do while este ca instructiunile dintre { } se executa cel putin o data! (chiar daca conditia de dupa cuvantul cheie while nu este satisfacuta). In contrast, in cazul buclei WHILE, daca conditia nu e adevarata, instructiunile dintre { } nu o sa se execute deloc.

### 1. Transcrieţi programele aferente temelor de lucru individual din laboratorul anterior 
(Laborator 7 – Instrucţiuni de ciclare – partea I-a), înlocuind instrucţiunea for de la cicluri mai întâi cu instrucţiunea
while şi apoi cu instrucţiunea do while.

```C
//Transformare for in while si do while
int i;
for(i = 0; i < n; i++) {
  //instructiuni
}
//-------------------------------------

//echivalent cu

int i;
i = 0;
while(i < n) {
  //instructiuni
  i++
}
//--------------------------------------

//echivalent cu
int i;
i = 0;

do {

  if(i >= n) { //poti sa verifici ca prima data cand i intra in bucla (dupa "do {") sa nu 
               //fie o valoare "ilegala" (care nu satisface conditia din while)
    break;
  }
  //instructiuni
} while(i < n);

```

---

### 2. Să se scrie un program care realizează în mod repetat următoarele:
- Citeşte un număr întreg de la tastatură;
- Determină şi afişează divizorii numărului citit;
- Determină şi afişează numărul de divizori obţinuţi;
- Dacă numărul este prim, afişează un mesaj corespunzător.
Exemplu: pentru n=20 , divizorii sunt: 1, 2, 4, 5, 10, 20, numărul divizorilor: 6

### Hints:
1. Citire repetata a ceva -> poti sa folosesti functia scanf ca si conditie.
```C
while( scanf("%d", &numar) ) {
}
```
2. Determinarea divizorilor

```C
//Algoritm - pot sa iti explic de ce e asa  

int posibil_divizor = 1;
int numar_de_divizori = 0;

while( n < (numar / 2) ) {
  if(numar % posibil_divizor == 0) {
    //posibil_divizor si (numar / posibil_divizor) sunt divizori
    numar_de_divizori = numar_de_divizori + 1;
  } 
  n = n + 1;
}
```
3. Este prim?
```C
if(numar_de_divizori == 2) {
  //numarul este prim, pentru ca daca numar_de_divizori == 2, singurii 2 divizori sunt 1 si el insusi
}

```

---

### 3. Se citeşte de la tastatură, caracter cu caracter, un text de maxim 50 de caractere. Citirea se opreşte
la întâlnirea caracterului punct. Să se determine:
- numărul de caractere citite;
- câte dintre acestea reprezintă una dintre cifrele de la 0 la 9;

### HINTS:
1. citirea unui caracter de la tastatura, initializarea variabilei care memoreaza numarul de caractere citite
```C
char caracter;
caracter = getchar();
int nr_caractere = 1;
```
2. intram in bucla daca 
```C
( (caracter != '.') && (nr_caractere <= 50) )
```
3. verificare in interiorul buclei daca caracterul reprezinta o cifra
```C
//conditie:
( (caracter >= '0') && (caracter <= '9'))
```
---

### 4. Se citesc de la tastatură, prin intermediul unui ciclu, mai multe numere naturale, până la scrierea
valorii zero. Pentru fiecare număr natural citit, să se determine şi să se afişeze reversul.

### HINTS:
1. citire numar si conditie de intrare in bucla (numar != 0);
2. intrare in bucla si aplicarea algorimului de revers:
```C
// Algoritm de revers:

int revers = 0;

while(numar > 0) {
  int ultima_cifra = numar % 10;
  revers = revers * 10 + (numar % 10); //adaugam cifrele invers in revers
  numar = numar / 10;
}

```
---

### 5. Se citesc de la tastatură, prin intermediul unui ciclu, mai multe valori naturale, până la scrierea
valorii zero. Să se determine şi să se afişeze numărul de citiri făcute până la oprirea ciclului. Pentru
fiecare valoare naturală citită, să se determine şi să se afişeze suma cifrelor.

### Hints:
1. initializarea unei variabile care sa numere citirile si sa contina suma finala
2. bucla do-while (pentru ca trebuie sa citesti oricum ceva inainte sa verifici conditia)
```C

int nr_citiri = 0;

do {
  // citesti numar
  // cresti numarul de citiri
  // algoritm de calculare a sumei cifrelor
} while (numar_citit != 0)
```
3. calculare suma cifrelor
```C
int suma = 0;
int numar_auxiliar = numar; (vrem sa nu stricam numarul original "numar" pentru ca o sa avem nevoie de el sa verificam conditia)
while(numar_auxiliar > 0) {
  suma = suma + numar_auxiliar % 10; //ultima cifra
  numar_auxiliar = numar_auxiliar / 10; //taiem ultima cifra
}
```
---

### 6. Se citesc de la tastatură, prin intermediul unui ciclu, mai multe numere naturale, până la scrierea
valorii zero. Să se determine şi să se afişeze cel mai mare dintre numerele citite.
 
### Hints:
1. citire ca si mai sus pana la afisarea lui zero
2. algoritm care gaseste maximul (cum am mai povestit si ai facut si la matrice ;) )
