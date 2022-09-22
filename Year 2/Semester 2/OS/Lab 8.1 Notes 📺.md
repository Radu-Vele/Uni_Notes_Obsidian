---
tags: [Notebooks/OS]
title: "Lab 8.1 Notes \U0001F4FA"
created: '2022-04-08T09:13:02.224Z'
modified: '2022-05-27T06:53:16.406Z'
---

# Lab 8.1 Notes :tv:

## 3 synchronization Labs
1. Semaphores
2. Mute Threads
3. Exercises

> For assignment only use 1 synchronization mechanism

## Recap Threads
Concurrency vs Parallelism
- concurrency issues => everytime we have concurrency these issues may occur.
- thread - abstraction for the CPU
- process - abstraction for PC
- scheduler - switch between threads running

Resource website: 
<a>dreadlock.empire.github.io

- non atomic operations are dangerous

## Remarks:
- don't forget to destroy the semaphores (.close( ),.destroy( ) );


## TODO
- study POSIX program sample
- Lab activity guidance
  1. sincronizare

  2. sincronizare sa nu depaseasca un anumit numar
  
  3. ***IMPORTANT*** alternative incremental

  *explanation*: permisiune (ca o minge care merge de la un thread la altul), cu 2 threaduri si apoi cu N threads
  e.g. 
  - cate un semafor pentru fiecare thread, thread urile isi apeleaza alternativ semafoarele apoi asteapta pe propriile semafoare

```
____
|T1| ___________-------------------___________________
____

____
|T2|-----------____________________-------------------
____
```
  - pentru N thread-uri facem un loop in care fiecare thread face post la urmatorul de dupa el (use indexes for a set of semaphores)

4. Probleme Assignment separat (four-fork problem) (sursa de bonus :dollar:)

### Problems 4, 5, 10 lab text - similar to the colocviu
- nu facem extraordinar de realist la probleme underspecified


## Evaluation :bear:

- Colocviu: probleme similare cu lab guidance. (pe categorii)
  - pe calculator aici probs
  - File System, Process Thread Communication, Inter Process Communication, Memory Management

- Exam: applied theory. 

# Lab Exam Code Examples

```c

#include <semaphore.h>

/**
* POSIX
* How to...
**/

/*
* Create, init, destroy, post, wait
*/

sem_t semaphore;
sem_init(&semaphore, 0, 3); // verify return

sem_wait(&semaphore);
sem_post(&semaphore);

sem_destroy(&semaphore);

/*
* Protect an area
*/

sem_wait(&semaphore);

/* PROTECTED CODE */

sem_post(&semaphore);


/*
* Named Semaphores
*/

//create

sem_t semaphore_named_1;
sem_t semaphore_named_2;

//init in process

semaphore_named_1= sem_open("/named1", O_CREAT, 0600, 0);
semaphore_named_2 = sem_open("/named2", O_CREAT, 0600, 0);

//close in process

sem_close(semaphore_named_1);
sem_close(semaphore_named_2);

//unlink

sem_unlink("/named1");
sem_unlink("/named2");


```
