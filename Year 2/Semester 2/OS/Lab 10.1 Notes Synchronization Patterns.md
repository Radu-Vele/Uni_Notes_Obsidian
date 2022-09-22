---
tags: [Notebooks/OS]
title: Lab 10.1 Notes Synchronization Patterns
created: '2022-05-02T07:05:35.681Z'
modified: '2022-05-27T06:58:36.232Z'
---

# Lab 10.1 Notes Synchronization Patterns

## Important for the exam
- we may be asked to write pseudocode that solves one of the problems

## Semaphores reminder
- Semaphore :link: Counter
```c
semaphore.increment(); //signal P() -- atomic
semaphore.decrement(); //wait V() -- atomic
```
- can be incremented/decremented by any thread
---
## 1. Rendez-vous
- synchronize 2 threads
```
  A   B
  |   |
  |   |
  |   |
  |  ---
  |   |
--------- meeting point
```
- A signals that it arrived and waits
- B signals that it arrived and waits

```c
#include <semaphore.h>
//A
sem_post(semaphoreB)
sem_wait(semaphoreA)

//B
sem_post(semaphoreA)
sem_wait(semaphoreB)
```

## 2. Barrier

- rendezvous with n threads (implementation semaphores / condition variables + mutex)
```C
  |   |   |
  |   |   |
  |   |  ---
  |   |   |
 ----------- meeting point for N == 3
  |   |   |
  |   |   |
```

```c
struct barrier {
  int cnt;
  mutex lock;
  cond_var cv;
  int N;
}

/*
* thread enters barrier
*/
void enter(barrier b) {
  lock.acquire();
  b.cnt++;
  if(b.cnt == N) {
    cv.broadcast();
  }
  else {
    cv.wait();
  }
  lock.release();
}
```

## 3. Producer-Consumer
- used in event-driven programming
- 1 producer P, 1 consumer C
E.g:
P -> 5 elements/sec
C -> 2 elements/sec

- synchronization of the buffer between writing/reading

```c
       _________
P --> |         |
      | BUFFER  |
      |         |
C <-- |_________|         

or queue implementation
       _ _ _ _ _
 C <- |_|_|_|_|_| <- P

```
```c
struct Queue_Buffer {
  int cnt;
  E elements;
  semaphore sem;
}

pop(Queue_Buffer q, E element) {
  q.sem.wait(); //decrement;
  
  q.lock.acquire();
  //...dequeue
  q.lock.release();
}
push(q, E) {
  q.lock.acquire();
  //...enqueue
  q.lock.release();

  q.sem.post(); //signal
}
```

- if the buffer is finite, when full => producer should be stopped
  - use another semaphore

## 4. Readers-Writers

```c
struct RW_lock{
  readers
  writer
  //acquire shared
  //acquire exclusive
  //release
}

if(reader) {
  if(rw_lock.writers == 0) {
    rw_lock.readers++;
    acquireShared();
    //...
    release();
    rw_lock.readers--;
  }
  else {
    //wait until writer leaves
  }
}
else {
  if(rw_readers > 0) {
    //wait until there are no readers
  }
  else {
    rw_lock.writers++;
    rw_lock.acquireExclusive();
    //...
    rw_lock.release();
  }
}
```
- problem: starvation of the writer => give priority to a writer

```c
struct RW_lock{
  int readers
  int writers
  int waiting_writer //priority variable
  //functions:
  //acquire shared
  //acquire exclusive
  //release
}

if(reader) {
  if(rw_lock.writers == 0) {
    if(rw_lock.waiting_writer) {
      //block;
    }
    rw_lock.readers++;
    acquireShared();
    //...
    release();
    rw_lock.readers--;
  }
  else {
    //wait until writer leaves
  }
}
else {
  if(rw_readers > 0) {
    //wait until there are no readers
  }
  else {
    rw_lock.writers++;
    rw_lock.acquireExclusive();
    //...
    rw_lock.release();
  }
}

//more accurate in the book + turnstile solution
```
## 4. Dining Philosophers

# TODO:
- problemele is cam ca si data trecuta

# Lab Exam Code Examples

```c
/**
* How to...
**/

//Study problems patterns
```

