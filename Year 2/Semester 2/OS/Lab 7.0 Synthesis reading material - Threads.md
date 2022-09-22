---
tags: [Notebooks/OS]
title: Lab 7.0 Synthesis reading material - Threads
created: '2022-04-01T05:54:23.818Z'
modified: '2022-04-01T09:33:17.098Z'
---

# Lab 7.0 Synthesis reading material - Threads

Linux Threads Library ***PTHREADS*** :penguin:

- `somehow similar to processes`

## 1. Create a thread

```C
#include <pthread.h>
/*
* returns 0 if success / possitive value = error code
*/
int pthread_create ( pthread_t* idThread, //mem address of identifier ///ca la dir ish
  const pthread_attr_t* threadAttributes, //mem address of a structure containing thread attributes -> NULL = default
  void* (*thread_routine)(void*), //mem address that thread executes
  void* arg); //arg passed to function by thread
```
- `porneste un thread total independent de la o anumita adresa - thread_routine`

***Lifecycle***: thread is created and executes it function then it dies

- the *main thread* executes main function (if it dies all the other ones will die) 
```C
void* thFunction(void* arg) {
  int* val = (int*) arg;  ///don't forget to cast to proper type
  printf("Thread with argument %d\n", *val);
}

main() {
  pthread_t th1;
  int arg1 = 1;
  pthread_create(&th1, NULL, thFunction, &arg1);
  pthread_join(th1, NULL); //wait for the termination of th1
}
```

:heavy_exclamation_mark: When compiling a program with threads we must use:
```
gcc progr.c –lpthread –o progr.exe #compiler links the library /// to add in vscode if you wanna
``` 

## 2. Thread's ID
- unique identifiier (got by create function)
- could be obtained by functions

```C
#include <pthread.h>

pthread_t pthread_self(void);

int pthread_equal( pthread_t thread1, pthread_t thread2);

#include <sys/types.h>

  pid_t gettid(void);
```

## 3. End thread's execution
```C
#include <pthread.h>

void pthread_exit(void *retval); //returned info ///finish the thread

#include <pthread.h>
int pthread_cancel(pthread_t thread); //termination of a thread by another thread (both are in the same process)
```

Information about termination status:
- the returned value of the function
- retval if pthread_exit is called

```C
#include <pthread.h>
int pthread_setcancelstate(int state, int *oldstate); //permission of a thread to be terminated by another thread
//PTHREAD_CANCEL_ENABLE
//PTHREAD_CANCEL_DISABLE
```
- a thread could be canceled immediately or wait until a cancel point
- `won't use the cancel stuff`

```C
#include <pthread.h>
int pthread_setcanceltype(int type, int *oldtype);
//PTHREAD_CANCEL_ASYNCHRONOUS
//PTHREAD_CANCEL_DEFERRED
```

- the cancel point are defined by POSIX standard whnere the thread is put in waiting
```C
//pthread_join, pthread_cond_wait, pthread_cond_timedwait,
//sem_wait, sigwait, sleep
//pthread_testcancel - explicitly for canceling

#include <pthread.h>
void pthread_testcancel(void);

//Cancel state: PTHREAD_CANCEL_ENABLE
//Cancel type: PTHREAD_CANCEL_DEFFERRED
```

- PTHREAD_DEFERRED protects threads that contain valuable (global) sections of code and shouldn't be canceled

- functions that are executed at termination are in LIFO logic

```C
#include <pthread.h>

void pthread_cleanup_push(void (*routine)(void*), //function to be exec
                          void* arg); //arg of the function
void pthread_cleanup_pop(int execute); //execute/not the function popped

//Use the above function together!!
```

## 4. Wait for thread to end

```C
int pthread_join(pthread_t th, void **thread_return); //block execution of calling thread until the end of th
//thread_return - information about termination state
```
The join function could be called only once for a thread, and ONLY for the threads for which the system has information about their termination state.

- `poate sa astepte doar dupa un anumit thread`
- `poate returna un pointer dat de functia exit`

## 5. Set thread's attributes
- create a DS that will be passed at the creation of the thread
```C
#include <pthread.h>

int pthread_attr_init(pthread_attr_t *attr);
int pthread_attr_destroy(pthread_attr_t *attr);

#include <pthread.h>

//atributes that deal with the possibility to call the join function
int pthread_attr_setdetachstate(pthread_attr_t *attr,
                                int detachstate);
//THREAD_CREATE_DETACHED
//PTHREAD_CREATE_JOINABLE

int pthread_attr_getdetachstate(const pthread_attr_t* attr,
                                int *detachstate);

//other information about the attributes
//pthread_attr_getstacksize and pthread_attr_setstacksize;
//pthread_attr_getstackaddr and pthread_attr_setstackaddr etc.
```

- Detached thread = No information about its termination status (all allocated resources will be freed)

```C
#include <pthread.h>
int pthread_detach(pthread_t th);
```

## 6. Relationship Threads - Processes
>A signal could be only sent to a process and not to a thread of that process. :heavy_exclamation_mark: (normally :smile:)
- in linux Threads are somehow lightweight processes
- threads and processes have mechanisms to block or allow signals using **Masks**

What if a thread of a process calls fork( ) ?
> Only the calling thread is active in the child process (and not all threads of the parent process)
- the child process ends when the thread ends
- solve fork issues with pthread_atfork( ) function that specifies what functions to be executed both in parent and child process before and after fork( ).
- if atfork( ) is called multiple times, a set of function will be called (in *LIFO* order)
```C
#include <pthread.h>

pthread_atfork( void (*prepare)(void), //function exec in parent before a new process is created
                void (*parent)(void), //fun exec in parent before fork finishes its execution
                void (*child)(void)); //fun exec in child before fork finishes exec
```

## Functions
|name|description|
|-|-|
|pthread_create | creates a new thread|
|pthread_join| calling thread waits for the termination of the arg|
|pthread_self|get thread's ID|
|pthread_equal|compare IDs|
|gettid|linux-specific|
|pthread_exit| terminate thread|
|pthread_cancel|terminantion of a thread by anothre thread|
|pthread_setcancelstate|allow thread to be terminated by other threads|
|pthread_setcanceltype|determine when to cancel thread|
|pthread_cleanup_push|add function to be executed whenn thread terminates|
|pthread_cleanup_pop| pop last fun added for termination|
|sigaction|set response to a signal|
|pthread_sigmask|define a mask for a thread|

