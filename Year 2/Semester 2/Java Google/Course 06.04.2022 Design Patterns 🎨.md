---
tags: [Notebooks/Java Google]
title: "Course 06.04.2022 Design Patterns \U0001F3A8"
created: '2022-04-06T16:05:55.336Z'
modified: '2022-05-02T06:58:41.153Z'
---

# Course 06.04.2022 Design Patterns :art:

Git Saleh: https://github.com/Mahagney/GAD-JAVA-2022

## Design Patterns:
> Role: provide general solutions to problems that are often met.
---
## **I. Creational**
- essentially trying to make use of composition while instantiating object

## :closed_lock_with_key: Singleton
> Use ONLY one instance of a class: private constructor, private static instance variable, public static method

### Approaches
|||
|-|-|
|Eager Initialization| the instance is created anyway at class loading|
|Static block initialization|same as upper but we can use a try catch|
|Lazy Initialization|like the one described in the note after the Singleton subtitle (thread dangerous)|
|Thread-safe|make the getInstance method `synchronized`|
|Thread-safe (2)| use a double lock, but the same mechanism|
|Bill Pugh|Use a helper class that does the initialization - loaded only when someone calls getInstance()|
|Enum| Enum is initialized only once always - solves serialization and reflection issues|

### Example:
- db Connection class

## :factory: Factory (virtual constructor)

> Ne ajuta sa instantiem obiecte (fabrica) definind o interfata, dar lasa subclasele sa decida ce clasa sa instantieze.

> Separam crearea obiectelor de client code

### Example:
- PizzaStore

## **:factory:FactoryMethod

- amanam instantierea catre subclase (ele decid ce obiecte sa creeze)
- o clasa separata care contine

```java
getInstance(String type) {
//verificam de ce tip e si instantiem ce trebe
}

/**
* In pizza example
*/
createPizza() {

}
```

## ***:factory: Abstract Factory
> O interfata factory care e implementata de alte clase de tip Factory
- `Head-First-Design-Pattern book`

.
.
.

:question: Difference between factory method, abstract factory and factory 
.
.
.

## :hammer: Builder
> For complex objects that only have a few mandatory attributes we can use a builder. Builder has a constructor with its main attributes as parameters, and setters for the other attributes.

- avoid having a constructor with many parameters
- separate building from the detailed assembly of the object
- punem atributele fara care nu poate exista in constructor

### Example:
- helicopter that can have many attributes
- car

## :pencil: Prototype
> Specify the kinds of objects to create (prototype) => all instances are created by cloning the prototype

- careful about deep and shallow copies in case of classes that contain references to other classes
- implement `Cloneable` and override `.clone()`

### Example
- dog with the leash

.
.
.

---


## II. ***Structural***
- deal with combining classes into larger libraries or so

## :electric_plug: Adapter
> Adapt interfaces so that objects can work together

- diff: class or object adapters

### Example
- the mobile charger adapter

## Composite :deciduous_tree:
> Allows us to compose objects such that lients treat compositions of objects like insividual objects

### Example:
- in a food menu there are products and daily menus (collection of products). But daily menus are also products

## Proxy :bird:
> Access an object through the surrogate (proxy) instead of directly accessing it (the object could be remote).

### Example:
- proxy copy-on-write (postpone the copy process of a large object to the time the object is modified).
- remote report generator for a machine

## Flyweight :ant:
> Avoid creating immutable objects more times than necessary by storing them in the same place.

### Example:
- string pool

## Facade :house:
> If we have a subsystem, a facade provides the means to interact with it through a higher-level interface instead of direct access

### Example:
- a tv remote for a home cinema

## Bridge :bridge_at_night:
> Separate an abstraction (interface) from its implementation 

## Decorator :christmas_tree: 
> Add attributes (responsabilities) to an object dynamically

- modul in care obiectele se compun in structuri mai mari
- foloseste interfaces + inheritance

### Example:
- christmas tree
- coffee shop

.
.
.

## III. ***Behavioral***

## Template Method

## Mediator

## Chain of Responsibility

## Observer

## Strategy 
- are scopul de a defini o familie de algoritmi pe care o grupeaza.

## Command

## State

## Visitor

## Iterator

## Memento (token)


## TODO:
- Sa ne gandim la 2 probleme pe care putem aplica cate und design pattern
  - create in the same repo a new package "proiect" -> new package "design pattern name" -> add implementation and `readme.md`
