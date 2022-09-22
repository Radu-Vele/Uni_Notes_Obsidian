---
tags: [Notebooks/PT]
title: Lab 4
created: '2022-03-10T07:45:19.377Z'
modified: '2022-03-10T13:29:48.289Z'
---

# Lab 4

# Assignment 2. Java Threads

## Thread = fir de executie
- linked to computer architecture
- in basic program -> sequential instructions (in code segment) => thread
- we need at least 1 thread (starts in main)
- the program runs the process

 ### **[thread + memory => process]**

>Our goal: 
To Run multiple programs on a single processor at the same time

- multi-core processors (not our aim as a single core can run parallel threads)
- processes vs threads:
  - *process*: individual memory area
  - *thread*: shared memory

## Java threads

- thread = object
- JVM makes a fork when a thread is started (thread.start())
- suprascriem run function, cand pornim thread-ul apelam run => incepe executia in paralel cu punctul in care eram in main
- manage threads (concurrency control), apar suprescrieri de valori => fecked up => implement semafoare si lacate 
- synchronize - keyword that allows only one thread to access the marked area => thread-safe code. Sunt DS sincronizate by default (vector). 

**! ArrayList nu e sincronizat**


```
//Code:

class MyThread extends Thread {
}

MyThread t = new MyThread();
t.start();

//-------------------------------

class MyThread implements Runnable {
}

public static void main() {
  MyThread t = new MyThread(new Mythread);
  t.start();
}

//-------------------------------

void run() {
  while(!done) { //exiting the run
    //...
    if(COND) done = true; //COND poate sa depinda de o variabila din alta clasa (shared mem)
   //....
   thread.sleep(miliseconds) //to observe how the thread runs
  }
}
```

## TODO: 
- create a thread class and start some instances of it, observe how it works
- use thread.sleep(ms) function
