---
tags: [Notebooks/OS]
title: "Lab 9.0 Synthesis reading material - Locks & Condition variables \U0001F512"
created: '2022-04-15T07:09:57.697Z'
modified: '2022-04-15T09:31:23.581Z'
---

# Lab 9.0 Synthesis reading material - Locks & Condition variables :lock:

`>> annotations <<`

## PTHREADS library synchronization
1. ***Mutex*** (Mutual Exclusion) `aka the most important sync mechanism` :astonished:
`Differences w.r.t Semaphores: `
`- only one thread can run at a time`
`- a mutex is OWNED by a thread (a semaphore could be V() by any thread)` :key:

2. ***Condition Variables***
> Used to synchronize only the execution of threads within a process (not inter-processes)

`- `

## Mutexes

```C
// Initialization

#include <pthread.h>

pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER; // predefined  constant to initialize with implicit values

/**
* @param: mutex = id of the mutex
* @param: attr = the address of a struct of attributes
*/
int pthread_mutex_init (pthread_mutex_t *mutex, const pthread_mutexattr_t *attr); //explicit initialization

int pthread_mutex_destroy (pthread_mutex_t *mutex); // destroy mutex

```

### Attributes of mutexes
Use a variable to store the attributes. If we call the init function the attributes are not allocated memory, so first we need to call init mutexattr.
```C
#include <pthread.h>

pthread_mutexattr_init (pthread_mutexattr_t *attr); //initialize the variable

/**
* Destroy mutex structure of attributes 
*/
int pthread_mutexattr_destroy ( pthread_mutexattr_t *attr);
```

Getting and setting the values of attributes
```C
#include <pthread.h>

int pthread_mutexattr_settype (pthread_mutexattr_t *attr, int kind);

int pthread_mutexattr_gettype ( pthread_mutexattr_t *attr, int *kind);
```
|Attributes||
|---|----|
|PTHREAD_MUTEX_FAST_NP||
|PTHREAD_MUTEX_RECURSIVE_NP||
|PTHREAD_MUTEX_ERRORCHECK_NP||

```C
// Other ways of defining
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

pthread_mutex_t mutex = PTHREAD_RECURSIVE_MUTEX_INITIALIZER_NP;

pthread_mutex_t mutex = PTHREAD_ERRORCHECK_MUTEX_INITIALIZER_NP;
```

### Lock MutEx
- ensure mutual exclusion by locking the mutex => all the other threads are put into a waiting state
```C
#include <pthread.h>
int pthread_mutex_lock (pthread_mutex_t *mutex);

//this one doesn't suspend the calling thread if the lock cannot be locked( :) )
int pthread_mutex_trylock (pthread_mutex_t *mutex);
```

### Unlock MutEx
```C
#include <pthread.h>

int pthread_mutex_unlock (pthread_mutex_t *mutex);
```

### Example Mutex :mute:
```C
/* The function which creates a mutex */
void createMutex(pthread_mutex_t *mutex) {
  pthread_mutex_init(mutex, NULL);
}

/* The function which modifies a variable */
/*Mutual exclusion access of the variable is ensured*/
void increment(pthread *mutex, int *variable) {
  pthread_mutex_lock(mutex); // locking the mutex
  (*variable)++; // exclusive access
  pthread_mutex_unlock(mutex); // unlocking the mutex
}

/* The function which destroys a mutex */
void destroyMutex(pthread_mutex_t *mutex) {
  pthread_mutex_destroy(mutex);
}
```

## Condition Variables
> Synchronize threads based on the values of some common variables

`- unlike semaphores, they don't hold an internal state`

### Init and delete

```C
#include <pthread.h>

pthread_cond_t cond = PTHREAD_COND_INITIALIZER; //implicit

int pthread_cond_init (pthread_cond_t *cond, const pthread_condattr_t *attr); //explicit

int pthread_cond_destroy (pthread_cond_t *cond); //delete

```

### Attributes

```C
#include <pthread.h>

int pthread_condattr_init (pthread_condattr_t *attr)
int pthread_condattr_destroy (pthread_condattr_t *attr);
```

### How to put threads in a waiting state?
- use pthread_cond_wait or pthread_cond_timedwait.

```C
//blocks the thread for an indefinite period of time (until call of the function pthread_cond_signal i.e. condition is fulfilled)
int pthread_cond_wait (pthread_cond_t *cond, pthread_mutex_t *mutex);

///indicates a time for which the thread is in the waiting queue
int pthread_cond_timedwait ( pthread_cond_t *cond, pthread_mutex_t *mutex, const struct timespec *abstime);
```

### Why do the functions have a mutex parameter? 
> :heavy_exclamation_mark: The condition variables are always used in code regions protected by mutexes

- that's because the condition variable imposes concurrent access to itself and needs to be protected

### How to wake the threads up?
- another thread calls pthread_cond_signal

```C
#include <pthread.h>
//Take out a thread from the waiting list
int pthread_cond_signal (pthread_cond_t *cond);

//Take out all threads from waiting queue of a condition variable
int pthread_cond_broadcast (pthread_cond_t *cond);
```

### Producer consumer problem example:
```C
#define DIMBUFFER 100
int buffer[DIMBUFFER];

int msgNo = 0;// nr. of unread messages
int indexProd = 0; // index for adding messages
int indexCons = 0; // index for reading messages

pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t empty = PTHREAD_COND_INITIALIZER;
pthread_cond_t full = PTHREAD_COND_INITIALIZER;

/* The function called by the producers */
/* Mutual exclusion access */
void produce(int item) {

  pthread_mutex_lock(&mutex);// lock mutex

  while (msgNo == DIMBUFFER) // if buffer is full
    pthread_cond_wait(&full, &mutex);

  buffer[indexProd] = item;// add message

  // update producer index
  indexProd = (indexProd + 1) % DIMBUFFER;

  // increment nr. of unread messages
  msgNo++;

  // wake up a consumer
  pthread_cond_signal(&empty);
  pthread_mutex_unlock(&mutex); // unlock mutex
}

/* Function called by the consummers */
/* Mutual exclusion access*/
void consume(int *item) {

  pthread_mutex_lock(&mutex); // lock mutex

  while (msgNo == 0) // if buffer is empty
    pthread_cond_wait(&empty, &mutex);

  *item = buffer[indexProd]; // read message

  // update consummer index
  indexCons = (indexCons + 1) % DIMBUFFER;

  // decrement nr. of unread messages
  msgNo--;

  // wake up a producer
  pthread_cond_signal(&full);

  pthread_mutex_unlock(&mutex); // unlock mutex
}

```

## Executing a function only once
- for functions that need to be called only once (independent of the number of threads that "by-pass" it) we can use the pthread_once mechanism

```C
#include <pthread.h>

pthread_once_t once_block = PTHREAD_ONCE_INIT;

//associate the variable a function whose calls will be made through the pthread_once mechanism
int pthread_once ( pthread_once_t *once_block, void (*init_routine) (void));
```
