---
tags: [Notebooks/Java Google]
title: Course 18.04.2022 Collections
created: '2022-04-04T15:29:20.708Z'
modified: '2022-04-18T17:37:42.511Z'
---

# Course 18.04.2022 Collections

## ToC

# Introduction

> Collection - container that groups similar objects

- Examples:

Array - group of objects having the same type

--> actually a memory area having a certain number of objects (references to objects) of the same type

--> not really used because of lists (fixed space, no predefined)

```java
Car[] cars = new Car[](); //
Car car = new Car(); //a new car object is stored in the heap
cars[0] = car; //a reference to the memory area is stored in cars[0]
```

## Access
### Random
- can access any element in the DS
- e.g. Arrays
### Sequential
- can access elements one by one
- e.g. Linked Lists

## Cursors
### Iterator
- ajuta la parcurgerea colectiilor fara acces la implementare
- concurrent modification - nu sunt permise (se bazeaza pe counter-ul intern al colectiei)
  - solution: **Iterate over a copy** (CopyOnWriteArrayList)
  - solution: Use iterator.remove() (only removes the current element)

fail-safe: ConcurrentHashMap

Conclusion: removing from lists has its limits

Alti iteratori: 
- ListIterator (bidirectional), 
- Spliterator (supports parallel processing of data)

## Types of Lists

### ArrayList
- has an array as backing data structure
- (-) inserting is difficult, cost++ (realloc + reposition elements)
- (-) appending is difficult
- (-) many reallocs (with double size of the initial array)
- advantage over LinkedLists = accesing data;

### LinkedList
- (+) easy to insert inside the list 
- (-) access more costly (very slow)

## Set
- no duplicate elements

## Queue
- priority queue
- linked list couls be used
- concurrent implementations (BlockingQueue)

## Map
> Mapare key-value


## Interfaces

## GIT
- reset
  - soft (LR)
  - mixed (Staging + LR)
  - hard (Local area)

## TODO:
- from Set next time.





