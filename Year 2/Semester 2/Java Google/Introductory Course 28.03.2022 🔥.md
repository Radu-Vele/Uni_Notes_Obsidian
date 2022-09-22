---
tags: [Notebooks/Java Google]
title: "Introductory Course 28.03.2022 \U0001F525"
created: '2022-03-28T15:28:54.313Z'
modified: '2022-03-28T17:50:50.795Z'
---

# Introductory Course 28.03.2022 :fire:

## Lesson Outline
1. Organizatoric Stuff
2. Git
3. Simple java program
4. Arrays

## Organizatoric stuff 
- Designed Pathway: `Java` --> `Android_Course`
- My stuff: Java 17, IntelliJ
- Compiler: javac
- read documentation on javadocs `ctrl + F` 
- cursurile disponibile

## GIT :cactus:
>Cum luăm cod de pe un remote repository
- fetch
- merge - adaugam in directory-ul nostru
- pull - does both of the upper two
```
git commit -a // both add and commit
```

## Java Programs
### Compilare
- fisier `.java` => **compilare** => `.class` (bytecode care poate fi rulat pe un os cu JVM instalat) => **run code**
- Java => Platform Independent thanks to JVM

## Objects vs Primitives
> Objects - class instances -> capitalized

> Primitives - basic data types -> lowercase

- Wrapper class - takes a primitive data type and creates a class with it
- inBoxing, outBoxing

## Arrays
```java
int[] array; //declare array
anArray = new int[3]; //instance of array --> on heap
```

- byte data type -> can encode 0 to 255

> Remark: Java Promotion Rules: byte, short, char promoted to int when operations are performed

--> solution: use casting

## String
- some special properties in Java daca nu folosim 'new'.
- immutable
- stored in a pool of Strings for optimization
- daca avem un string care deja exista si vrem sa mai avem o variabila care are referinta la un string cu aceleasi caractere, in memorie nu se mai face un nou obiect String (daca nu apelam new String("something"));

- if we don't want to use the string pool use StringBuilder class

### System methods:
- arrayCopy

## Operators
```java
//if operator
cond ? var1 : var2
```

## Equals vs '=='
- if we use the == operator for names of classes instances, only the addresses are compared whereas .equals compares the content of the object - ish *see Lect7 PT Course

## Memory
- Stack - code, primitives, static memory + thread exec + contine adresele de memorie spre heap objects
- Heap - objects (new)
- o metoda apelata o sa ocupe memorie in stack

## Next time:
- annotations + other basics 
