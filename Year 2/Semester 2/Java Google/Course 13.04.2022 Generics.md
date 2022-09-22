---
tags: [Notebooks/Java Google]
title: Course 13.04.2022 Generics
created: '2022-04-13T15:24:12.934Z'
modified: '2022-04-13T17:17:12.714Z'
---

# Course 13.04.2022 Generics

## Raw Types
- don't specify the type of parameters
```java
List<T> //T is a raw type
```
- if T is not specified, cast shall be used (cast = garantie de la programmer ca ala e data type-ul folosit)
- T este definit la compileTime
- For generalizing we could also use Object class, but in that case we could't call specific methods

> Allow.s code to be generalized (create a class that could contain collections of different objects)

- can't be used with primitives

### Generic methods - used as well

```java
public <T> int sum(T param1, T param2)
```

- we can also limit the type to an *extent* using the keyword *extend*. => we can also extend a class and multiple interfaces 
\+ Advantage: use the methods of the bound class for the type in the generic implementation

```java
class D <T extends ClassName & Interface1 & Interface2> {

}
```

### Inference 
- the compiler looks at the parameter types and assigns the proper type (when the param don't have the same time the compuler looks for the most recent common ancestor)
- for wildcards we can't really add stuff

### Backward compatibility
- cand aducem un update ar trebui sa ne asiguram ca o sa mearga tot ce mergea inainte.
- merg niste chestii din jdk 1.5 de dinainte de raw types, dar nu e ok sa folosim

### Type Erasure

-> Heap pollution
Rezulta din Type erasure. In heap vom avea tipuri unexpected. (solve by using the generic type as much as possible)

##  Wildcard
- <?> unknown type used as a param/field/local var/return type
- solves the situations when -
- could be:
a. upper bound (extends) - superior limit
b. lower bound (super) - inferior limit
