---
tags: [Notebooks/PT]
title: "Lab 9.0 Assignment 4 Presentation \U0001F354"
created: '2022-04-14T07:21:23.462Z'
modified: '2022-05-05T07:49:33.097Z'
---

# Lab 9.0 Assignment 4 Presentation :hamburger:

## ToC Contents
1. **Collections framework** 
1.1 Maps
2. **Stream Processing** (JSP)

3. **Design patterns**
3.1. Observer
3.2. Composite

4. **Serialization**

## 1. Collections framework
- implemented data structures - optimal.

```
e.g. Find first k minimum elements in an array
Dummy solution: Iterate through array and keep the minimum numbers into an array that will be searched at each step O(n * k).

Better solution: Build a Heap and extract first k elements.
```

## Map
- used as a hash table.
- obiect -> numar -> numarul e inserat in DS
```java
/*    MAP <K,V>
* 
* - interface like a dictionary key-value
* - used in caching servers
* - search for key get value
* - essentially a hashTable (searching in O(1))
* - hash() function restricts the set of values to a set of keys
* - implemented as a list of <K,V> -> index = hash(hashCode(k));
*/

HashMap <K,V> implements MAP<K,V> {
}

// Map<Order, Collection<MenuItem>> => 2 pasi pentru a obtine index-ul
```
- Collisions - solved by **chaining** (sunt pusi arbori Red-Black)
- overrride equals(), hashCode(), hash(?)


Other DS: LinkedHashMap, HashSet;

- ne ajuta pentru a pastra ordinea inserarii comenzilor. 

### Remark!
> folosim un **TreeMap** (RedBlack Tree - balanced) - (inserare a n elemente O(nlogn)). Also LinkedHashMap


### Set
- implemented 

## 4. Serialization
- similar view to writing to a file in C
- scrie un obiect intreg in fisier, care poate fi si citit.

```java
...implements Serializable {

}
```
> For composite objects all sub-objects need to be serializable :heavy_exclamation_mark:

### Stream
- functional programming related (used in big data) & uses lambda expressions
- Operations
  - terminal (reduce, collect)
  - intermmediate (filter, map)
- codul se executa propriu zis doar la operatii terminale.

e.g.:
suma patratelor numerelor impare dintr-un sir:
```java
int sum = list.stream().filter(x -> x % 2 == 1).map(y -> y * y).reduce(0, Integer :: sum);
                              param -> condition
```

# 5. Design Patterns

## 5.1. Composite
- we want methods to be called on simple and composite objects in the same way
- eventually we get to simple products (leaves of a tree)
- used for MenuItem

## 5.2. Observer
- maybe a frontend class is linked (observer) to a backend (observable) class s.t it reacts to changes in observable

```java
public class Observable {
  List<Observer> observers;
  public void addObserver(Observer newObserver) {
    observers.add(newObserver);
  }

  public void notifyAll() {
      for(Observer curr : observers) {
        curr.update();
      }
  }

}

//-----------------------------------------------

public class Observer {
  public void update() {

  }
}
```

## 5.3 Factory Method - in relation to Strategy

### Factory Method
- de exemplu cand vrem ca userul sa poata sa aleaga in ce tip de fisier sa salveze
- interfata care declara metodele de scris in clase
- implementari pentru fiecare tip de writer
- o clasa care e ca un "switch" si selecteaza ce tip de writer vrem


## TODO:
1. Study Map DS in Java


## General Remarks
- Layered Structure (like A.3), but the main difference is that we read and write to a text file rather than to a database. (we change the Data Layer).
- Caching.
