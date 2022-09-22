---
tags: [Notebooks/Java Google]
title: Course 20.04.2022 Concurrency
created: '2022-04-20T16:25:51.043Z'
modified: '2022-05-02T16:27:24.734Z'
---

# Course 20.04.2022 Concurrency

# Processes & Threads
### Process: self-contained execution environment
- are propriile resurse
- JVM - un singur proces

### Threads
- unit of execution
- share resources

### Daemon thread
- trebuie sa fie utilizate de alte thread uri (un timer, etc)

---
### Define a thread
- implement runnable
- extend Thread

### Pause
- .sleep
- .join - wait for another thread

### Interruption

# Synchronization
Errors:
- memory inconsistency 
  - memoria din main memory nu este actualizata cu ceea ce are un thread in cache-ul core-ului pe care il foloseste
  - two threads read the same data but don't view it consistently

- thread interference ()  
  - modifica aceeasi variabila si nu apuca unul sa scrie pana celalalt citeste
  - operatii din mai multi pasi

## Solutions
### "SYNCHRONIZE" (lock)
- makes a lock on the whole method / block / statement (intrinsic lock)
- there s an intrinsic lock on the object

### "Volatile"
- helps with memory inconsistency but *NOT* with thread interference
- write before read from memory;

### Atomicity

## Problems

## Broken Channel
Problems:
  - thread interference

### **Guarded Blocks**
```java
Object.wait() //suspend curr thread until another thread notifies it to change

Object.notify() //wake up a waiting thread

Object.notifyAll() //wake up all waiting threads
```

# Liveness
Our focus issues: deadlock, starvation, livelock

## Deadlock
- threads block each other

## Starvation
- a thread is unable to take *regular time* access

## Livelock
- threads work in parallel but depend on each other => remain in a loop


# Immutable objects
- build and cannot modify their state
- can't be inconsistent and can't cause interference

How:
- final private
- no setter
- no override for subclasses
- don't modify through methods
- don't share references to the mutable components of the object

# Lock Objects
- work like implicit -synchronized- locks
```java
class ReentrantLock {
  //...
}

trylock();
lock();
unlock();
```
- lock objects could impose *fairness* (order of threads)

# Executor


