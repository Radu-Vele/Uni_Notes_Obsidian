---
tags: [Notebooks/Tutoring]
title: "Functii + Recursivitate \U0001F4BB"
created: '2022-05-06T16:19:58.644Z'
modified: '2022-05-08T21:11:32.344Z'
---

# Functii + Recursivitate :computer:

## Declararea funcțiilor:
Modul în care se declară o funcție e descris in tabel:
| |tip_returnat| numele_functiei |(tip_parametru nume_parametru) {...}|
|-|-|-|-|
|ex 1 | int| maximul|(int a, int b) {...}|
|ex 2| void| printeazaUnVector|(int vector_de_printat[], int n) {...}|

```c
/**
* Exemplu de functie care extrage minimul dintr-un tablou si il returneaza
*/
int minimulDinTablou(int tablou[], int numar_de_elemente) {
  int i;
  int minim = tablou[0];

  for(i = 1; i < numar_de_elemente; i++) {
    if(tablou[i] < minim) {
      minim = tablou[i];
    }
  }

  return minim;
}


// Functia main
int main() {

  int a[] = {2, 5, 1, 5, 7};

  int minimul = minimulDinTablou(a, 5);

  printf("minimul din tablou este: %d", minimul);

}

```

## Recursivitate 
- abilitatea unei functii de a se chema în interiorul corpului ei; 



- Exemplu de problemă cu șir recursiv:

forumula de recursivitate : $S(n)=S(n-1)+ \frac{-1^{n}}{(2n+1)*3^n}$ (trebuie aplicată în funcția recursivă).

```c
/*
* @returnat: o variabila float
*/
float S_Recursiv(int n) {
  if(n == 0) {
    return 1;
  } 
  else {
    return S_recursiv(n-1) + pow(-1, n) / (2 * n + 1) / pow(3, n);
  }

}
```

:heavy_exclamation_mark: Atentie: pentru a nu avea o apelare infinită de funcții e nevoie să adăugăm o condiție de oprire. De exemplu, mai sus, (n == 0) este condiția de oprire.

---

## Exemple de probleme:
Funcții non-recursive:
Basic

1. Scrie o functie care parcurge un tablou si afiseaza pe ecran elementele pătrate perfecte.
2. Scrie o functie care primeste ca parametru lungimea laturii unui patrat si returneaza aria lui.

Mai grele putin

3. Scrie o functie care primeste ca parametri doua siruri de caractere si verifica daca acestea sunt identice. Daca sunt identice returneaza 1, altfel returneaza 0

Hint:
```c

//aici faci functia ceruta
int siruriEgale(//...
                      ) {
  //...
}

//codul din main
int main() {
  char sir1[6] = "Andrei";
  char sir2[5] = "Ardei";

  printf("Sirurile sunt egale (1=da, 0=nu): %d" siruriEgale(sir1, sir2));
}
```

```C
//cum sa parcurgi un sir de caractere

for(i = 0; sir_de_caractere[i] != '\0'; i++) {
  ...
}
```

Functii recursive:

4. Scrie un program care calculeaza al n-lea numar al lui Fibonnaci

Formula: $Fib(n) = Fib(n-1) + Fib(n - 2)$

5. ... de implementat functii recursive si pentru alte formule de recurenta:

ex: $X_{n} = 3X_{n-1} − 2X_{n−2}, \space \space X_0 = 0, \space X_1 = 1.$

