---
tags: [Notebooks/Java Google]
title: Course 30.03.2022 OOP
created: '2022-03-30T15:31:14.885Z'
modified: '2022-04-04T17:31:12.559Z'
---

# Course 30.03.2022 OOP

## TODO:
Quiz-urile in fiecare saptamana
### Recap:
- `git add` -> adaugam din working dir spre zona de staging (local)
- `git commit` -> din staging in local repository (local)
- `git push` -> din local repo in remote repo (remote - need web connection)
- `git fetch` -> din RR in LR 
- `git merge` / rebase -> din LR in WD
- `git pull` -> din RR in WD direct
- `git log` -> shows events over time

- **conflict** - s o modificat acelasi fisier la acelasi linie de 2 persoane
  - rezolvare: 
    1. *Merge* - se pun modificarile si poti sa alegi manual ce sa ramana => commit final cu toate modificarile 
    2. *Rebase* - commit urile paralele de pe un branch sunt reintroduse dupa commiturile de pe celalalt => main-ul nu mai e as expected => force push (dangerous)
## Today

## OOP + Notes from slides

## Class
- e.g. proiectul dupa care se creeaza ceva / schita
- constructor = modul de a crea obiecte, allocates space on heap

Contains: attributes (state), methods (behavior)

Method:
- methods - has signature (name + nr/name/order of param)
- method overloading (same name, different parameters)
- can return the specified type and its subclasses
- parameters = formal list of variables in the declaration
- arguments = actual values passed at function call
- varargs
```java
void m(Integer...i) // variable number of arguments
```
- primitive data types **immutable** i.e. if we send as parameter a primitive its value cannot be changed
- if we send a reference to an object (by value) its attributes could be changed in the method


Access control to fields
>**Reduce access as much as possible** (*private*)

- every instance of a class shares a class variable (in the same mem location)

Static fields

- ne spun ca o variabila apartin clasei
- o valoare care va fi aceeasi pentru toate instantele (characterizes a class not objects)
- any object can change the value of the static field 
- static + final => constant value
- private static initiallization - can reinitiallize
---

- `covariant return type` = a method specified to return a class object can return only an object of the that class / one of its subclasses

---
### Nested Classes
- declare a class within another class
- \+ more encapsulation 
- static
- vrem sa le folosim doar local

### Inner Classes
> Definite in interiorul altor clase, au acces la atributele si metodele clasei parinte

- non-static nested class
- associated to an instance of its enclosing class
- cannot define any static members

### Local classes
- are similar to them
- declared in methods


Shadowing field = use the name of the field for a parameter of the method (only in constructors or setters).

### Anonymous classes
> a class only used once that creates an instance of itself in its declaration (doesn't have a name)

- implementeaza o metoda pentru orice am avea nevoie

e.g. :
```java
// java anonymous class

public class Car {
  private Engine engine
  public void drive(Engine engine) {
    engine.drive();
  }
}

public class Engine { //inheritance
  public void drive(Engine engine) {
    this.engine = engine;
    System.out.println("Drive safe.");
  }
}

public class Main {
  main() {
    Car car = new Car();
    car.drive(new Engine());
    car.drive(new Engine() {
      @Override
      public void drive() { //in this case we overwrite drive() without declaring another class
        //super.drive() // access Engine usual function
        System.out.println("Drive fast using turbo");
      }
    }
  }
}

```

### Abstract classes
> can't be instantiated, can have abstract methods (no body)
- vor fi mereu super clase
- nu sunt "complete"

```java
public abstract class Car { 
  //are si cod spre deosebire de interfete
}

public class AudiA4 extends Car {
  @Override
  //method in the abstract class (bring our own implementation )
}

public class MercedesCClass extends Car {
  @Override
  //methods in the abstract class
}

public class Main {
  psvm() {
    Car car = new AudiA4();
    Car car1 = new MercedesCClass();
  }
}

```

***reminder***: Interfata: interactiune user - clasa
- interfetele segregare de responsabilitati (separare a functionalitatilor)
- abstract classes sunt pentru code reusability

> constructorul fara parametri se apeleaza automat, altfel trebuie sa chemam in child process `super(parametri)`

### Enum class
```java
public enum Planet {
  MERCURY(12, 12),
  EARTH(10, 9),
  JUPYTER(9, 0),
  MARS(11, 30);

  public final double mass;
  public final double radius;
  Planet(double mass, double radius) {
    this.mass = mass;
    this.radius = radius
  }

}
```

## Object
- instanta unei clase, e.g. un obiect concret

|Field|Methods|
|-|-|
|state|Behavior|

- steps
  1. Create a variable (stack) where the object
  2. Call new (alloc memory on heap)
  3. Constructor initiallizes fields values

## Interface

Ce punem in ea? :smile:
|Constante|public static final|
|-|-|
|inner classes|
|static methods|
|default methods|used in lambda functions|
|methods without a body|Integer getValue( );|

- *e.g. tastatura unui laptop, butoane radio* :radio:
- prin ele putem sa facem legam obiecte
- o clasa poate implementa mai multe interfete
- they group certain behaviours
- *de exemplu pentru un radio cu ceas am avea o interfata de radio, una de ceas, una de cititor de casete*
- ex. 2 : masina - 
  - interfata de sistem audio
  - interfata de caroserie
  - interfata dintre cutia de viteze si motor

- incapsulam functionalitatea si utilizatorul nu trebuie sa stie ce s-a facut inauntru


## Inheritance:

- Contract: child class ***is a*** parent class

>Static methods in interfaces are never inherited

`super` 
-> invoke everriden methods
-> refer to a hidden field

- Object class = The mother of all classes

e.g. **HIDING**

```java
public class Parent {
  public String field = "Parent 22";
  public static void m() {
      sout("Parent m method");
  }
}

public class Child extends Parent {
  public String field = "Child 10"; // >> hides the field parent
  public static void m() {
    Parent.m()
    sout("Child m method"); // >> it is not ovewriting, it is a hiding
  }

  public void printFields() {
    sout("Child field: " + field + " Parent field " + super.field);
  }
}


public class Main {
  psvm() {
    Child child = new Child();
    child.printFields();
  }

  //conclusion: la metodele statice nu este suprascriere, este hiding
}

```

Instance method vs Static method:
- I.M. se apeleaze pe instanta (overriding la inheritance)
- S.M. se apeleaza pe Clasa (hiding la inheritance) (respectiv pe tipul variabilei (reference type))
- daca incercam sa le combinam (static overrides instanta sau invers => *compile time error* :skull:)

### :heavy_exclamation_mark: Remark:
> Daca implementam doua interfete si vrem sa aplicam o metoda statica trebuie sa specificam din care interfata luam implementarea

### More of it in ***Lambda Functions***

---

### Object.clone( )
- implement Cloneable interface (else it throws CloneNotSupportedException)
- creates a "shallow" copy of the calling object (doar ne pune adresele de memorie ale atributelor daca nu suprascriem .clone( ) )

### Object.equals( )
- objects have the same value
- when overriden we need to override hashCode( )
- == compara adresele de memorie

### Object.hashCode( )
- returns the object's memory address in hexadecimal in Object class implementation
- by overriding we specify the location of the desired field (i.g)
- more of it at `Collections`
## Package

> Namespace of related classes and interfaces
- more rules in ppt
---

# OOP Features

## I. Encapsulation
- private fields (getters & setters)
  - solve by declaring superclass methods as final
  - extend mostly classes with abstract methods
- white-box reuse

- ascunderea implementarii folosind interfete:
  - declaram o variabila de tipul interfetei pe care o implementeaza clasa ei :cool: (deci nu mai vede metodele din clasa care nu sunt incluse in interfata)

- inheritance breaks encapsulation with some benefits-*ish* 

> Prefer composition over inheritance

## II. Composition
> `has-a` relationship
- assemble objects.
- Black-box reuse
- defined at runtime as object acquire references to each other
- careful with the design of interfaces

> Objects are accessed solely through their interfaces => no encapsulation break

Remark:
- Compile-time: (code -> byte code) -> Inheritance is visible
- Run-time: (execution of byte code) -> Composition is visible

## III. Delegation
- acts by using composition instead of inheritance and keeping the power of inheritance
\+ easier to compose behaviors at runtime

> Relatia dintre A si B este destul de "loose"

## IV. Polymorhpism

> Substitute object of matching interface for one another at runtime.

- works for abstract classes as well

### -> putem inlocui parintele cu copilul

- dynamic-binding (associate a request to an object at runtime)

### Types
1. Static 
    - early/compile time
    - done by method overloading (in the same class)
2. Dynaic
    - dynamic (runtime)
    - method overriding (in different classes) 

# Principles

## GoF
> 1. Program to an interface not an implementation

Results:
- low dependencies in implementation

> 2. Favor object composition over class inheritance

Results:
- small class hierarchies, keep class encapsulated
- unde e clar ca ar fi mostenire folosim mostenire

> 3. Designing for change
- achieved by design patterns 

## SOLID 

### ***S***ingle responsability principle
### ***O***pen-closed principle
### ***L***iskov substitution principle
### ***I***nterface segregation principle
### ***D***ependency inversion principle

### 1. S
- a class / method should have only 1 reason to change

### 2. O
- open for extension / closed for modification

### 3. L
- we could replace the supertype obj with any subtype obj whithout alteration of code.

### 4. I
- shouldn't depend on methods that are not used
- interfaces shall be split into more specific ones
e.g. Split Vehicle into Driving Vehicle, Flying Vehicle

### 5. D
- high-level modules should not depend on low-level modules
- abstactions should not depend on details
- nu folosim clase concrete in modulele high level

## Questions
- the D principles? :white_check_mark:
- secventele block code (diferenta intre static{} local{}) 
- casting intre superclass si subclass (cand e ok sa facem, si cand nu) (ce se intampla cand cast parent to child?) :white_check_mark: nu facem cast de la parinte la copil
- how does it work with final methods :white_check_mark: cannot be overriden by another class. 

- cand apelam constructorul unei clase care mosteneste o alta clasa se apeleaza initial constructorul superclasei? :white_check_mark: - da
