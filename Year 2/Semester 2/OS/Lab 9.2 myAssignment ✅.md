---
tags: [Notebooks/OS]
title: Lab 9.2 myAssignment ✅
created: '2022-04-26T08:43:27.864Z'
modified: '2022-05-13T08:31:17.816Z'
---

# Lab 9.2 myAssignment :white_check_mark:

## Tips:
- Thread barrier mai greutz:
  
  - the INIT function sends back a delay => too much synchronization offers TIMEOUT

  - when we call init on T10 we get a sleep during which the other threads may be leaving
  
  - cand T12 asteapta, trebuie sa se execute si alte thread-uri, dar sa ramana destule ca sa fie satisfacuta conditia.
  - solutie -> o problema din lab activity guidance + lab less classical lil book of semaphores
  
- different processes threads, nu avem nevoie de pipes: global semaphores (exemplu la semafoare program samples)

```C

#include <semaphore.h>
int a; # 
//named semaphore
sem_open(...,...,fara O_CREAT);
//remove it 
sem_unlink(...)
```

## Conventions & Info

## TODO:
### 1. Compile and run :white_check_mark:
### 2. Process Hierarchy :white_check_mark:
- parents should wait for their children
- hierarchy graph given
### 3. Sync threads from the same process :white_check_mark:
- P6 creates 4 other threads :white_check_mark:
- Conditions: :white_check_mark:
3.1. T6.0 musn't terminate before the other 4 threads
3.2. T6.2 (START) --> T6.4 (START) --> T6.4 (TERMINATE) --> T6.2 (TERMINATE)

### 4. Threads Barrier - *TO_FINISH*
- P3 creates 50 threads :white_check_mark:
- Conditions:
  - 4.1. The main thread waits for the other 50 to terminate :white_check_mark:

  - 4.2. At most 4 threads could be running simultaneously :white_check_mark:

  - ***4.3 Thread T3.10 could only end while 4 threads (including itself) are running***

```c
/*
Threads barrier ideas:
Different functions:
- normal threads have a function they execute where they pass in groups of 3
- t10 executes another function
- t10 enters the function => it stops the threads in the other function until there are 3 of them
*/

//49 threads
//reuseable barrier
void normalFun() {
  sem_wait(3);
  info(BEGIN)
  mutex.lock();
  count++;
  if(count == 3) {
    sem_post();
  }
  if(totalThreads == 46 && still_care) //47 48 49 {
    sem_wait();
  }
  mutex.release();

  sem_wait();
  sem_post();


  mutex.lock();
  count--;
  mutex.release();

  sem_post(3);
}

//1 thread
void t10Fun() {
  info(BEGIN)
  semaphoreThreads_wait()
  semaphoreSpecial_wait()
  info(END)
  semaphoreThreads_signal()
}
```


### 5. Synchronize threads from  different processes :white_check_mark:
- P5 creates 4 threads

  - 5.1 The main threads waits for the other ones to terminate
  - 5.2 T5.1 must terminate before T6.1 starts, and T5.4 must start only after T6.1 terminates
