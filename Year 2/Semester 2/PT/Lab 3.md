---
tags: [Notebooks/PT]
title: Lab 3
created: '2022-03-02T18:32:22.070Z'
modified: '2022-03-09T06:39:20.989Z'
---

# Lab 3

### Feedback:
- return un polinom in functiile de operatii

### **Today**: 
- operatii 
- JUnit Tests (presented in pdf)
```
JUnit
-> se fac metode, utilizam assert (poate fi dezactivat la compilarea codului)
-> nu ajung instructiunile in executabil
-> o metoda de test pentru fiecare metoda definita (verificam daca rezultatul operatiei e bun)
```

## Interface
- minimal model: input de la tastatura, result, **quotient**
- afișăm polinomul ca string
- ar fi frumos să tratăm caz special x^0 = x;

## Adunare
```
polinomAdd(polinom1, polinom2)

-> copiem un polinom in rezultat
-> ca si interclasarea a doua liste
-> O(n^2)
```

## Subtraction

```
Adunare cu -1 * al doilea
```

## Multiplication

```
-> tot un for in for

-> ! Monoame de acelasi grad -> compressPolynomial
```

## *Division*

```
/*
Algorithm: A / B
-> luam monom de grad maxim A, impartim la monom maxim la B
-> assign cat si rest
-> scadem din A (cat * B)
-> deimpartit devine rest
-> construim catul pe bucati
-> return lista de polinoame list(0) = cat, list(1) = rest
*/

List<Polynomial> division(Polinom d, Polinom i) {
  List<Polynomial> res = new ArrayList<Polynomial>();
  List<Polynomial> cat = new ArrayList<Polynomial>();

  while(d.getGrad() >= i.getGrad()) { 
     Monom md = d.getMonomMax();
     Monom mi = i.getMonomMax();

     Monom mc = md.divide(mi); // o functie care imparte un monom la altul grad scazut,                          // coeficient impartit
    
     cat.add(mc);
     Polinom auxPoly = operatii.multiply(i, mc); 
     d = operatii.substract(d, auxPoly); // replace d with the result
  } 

  res.add(c);
  res.add(d);

  return res;
}



```

## Derivation
- un singur argument
```
-> modify each monomial
```

## Integration

- un singur argument

```
-> index++
-> adaugam o constanta 
```
