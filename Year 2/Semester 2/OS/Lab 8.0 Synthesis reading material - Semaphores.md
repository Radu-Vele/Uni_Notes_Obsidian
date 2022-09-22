---
tags: [Notebooks/OS]
title: Lab 8.0 Synthesis reading material - Semaphores
created: '2022-04-07T14:29:31.746Z'
modified: '2022-04-08T09:28:14.863Z'
---

# Lab 8.0 Synthesis reading material - Semaphores

> Semaphore = mechanism to synchronize the execution of the processes that concurrently affect the same shared resources.
They can be used also between **threads**, not only processes.

- A process can enter its critical zone only if all of the other processes allow it to.
- support process communicarion

`Abstraction:` mechanism used for a room to control how many people. When someone enters, one inserts a token, when they give a token back

> Semaphores are ATOMIC :dizzy:

Linux Semaphores
1. SystemV
2. ***POSIX*** -> we will use them

## Structure
- an integer and a waiting queue
1. Process asks for permission to enter its critical zone `P( )` 
2. Permission given
2.2. Value of semaphore is decremented
2.3. Process execution
2.4. Process finishes => sends a message to the semaphore `V( )`
2.5. Value of semaphore is incremented
3. The value of the semaphore is zero
3.1. The process is suspended and put inside a waiting queue
3.2. A permission is released
3.3. The process is waken up and receives permission

> Only change the value of the semaphore through a P( ) or V( ) (if we're not talking about the initialization)

- P( ) and V( ) are executed **atomically** -> The PRIMITIVES of the semaphore
- Atomicity solves the problem raised by the fact that the semaphore itself could be considered a shared resource.

### The initial value
- If the initial value is 1 => mutual exclusion
- if it is bigger than 1 => several processses can enter their critical zone.
- if 0 => all processes are blocked => **STARVATION** (or this is the case when semaphores are used as a means of communication <Producer-Consumer\>)

## Creating Semaphores
Semaphore = Resource of the system

```C
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/sem.h>

/**
* Create a semaphore
* @param: key - integer to identify a set of semaphores, predef as IPC_PRIVATE
* @param: optiuni - set to 0 if we want access to existing semaphores
*         different from 0 => or between IPC_CREAT, IPC_EXCL, ACCES_RIGHTS (rwxrwxrwx)
* @return: descriptor integer at success ( > 0) or -1 in case of failure
*/
int semget(key_t cheie, int nrSemafoare, int optiuni);


//if we want to use string for naming semaphores
ftok() //generates an integer based on the path to a file and another integer
```

## Operations on Semaphores

```C
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/sem.h>

struct sembuf {
  unsigned short int sem_num; // numar semafor (index)
  short int sem_op;// operatia pe semafor 
                   // > 0 => incrementation with the sem_op value
                   // == 0 semaphore value has to be zero (blocked until so)
                   // < 0 => decrementation by abs(sem_op) 
  short int sem_flg; // optiuni operatie 
                     // IPC_NOWAIT - if process is blocked => exit immediately the execution of the operation
                     // SEM_UNDO - "cancels" the operation previously made by a process that suddenly ends
};

struct timeval {
  time_t tv_sec;  // secunde
  long int tv_usec;// microsecunde
};

/* The calling process remains blocked until the operations can be executed
* @param: id - returned by semget
* @param: operatii - list of struct sembuf
* @param: nrOperatii - length of list
*/
int semop(int id, struct sembuf *operatii, unsigned nrOperatii);

/*
* The calling process remains blocked only for the time indicared by timeout
*/
int semtimedop(int id, struct sembuf *operatii, unsigned nrOperatii, struct timeval *timeout);

/*
* Initialize the value of the semaphore
*/
semctl()
```
> The first two functions could be used to make sure that two processes won't block each other.

## Controlling sets of semaphores

Set of semaphores :link: Data structure (info to manage the set)
```C
// Struct semaphore set
struct semid_ds {
  struct ipc_perm sem_perm; // permisiuni
  time_t sem_otime; // timpul ultimului apel al functiei semop
  time_t sem_ctime;// timpul ultimei modif. a structurii semid_ds
  unsigned long int sem_nsems; // nr. de sem. din set
};

// Struct Permisiuni
struct ipc_perm {
  key_t key; // cheia setului de semafoare
  ushort uid; // uid efectiv proprietar
  ushort gid; // gid efectiv proprietar
  ushort cuid; // uid efectiv utilizator creator
  ushort cgid; // uid efectiv utilizator creator
  ushort mode; // permisiuni
  ushort seq; // numar de secventa
};
```

```C
// Describes a semaphore
struct sem {
  ushort semval; // valoarea semaforului
  short sempid; // pid ultima operatie
  ushort semncnt; // nr. de procese ce asteapta ca val. semaforului sa creasca
  ushort semzcnt; // nr. de procese ce asteapta ca  val. semaforului sa devina 0
};
```
How to modify any of these data structures?
```C
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/sem.h>

union semun {
  int val; // SETVAL
  struct semid_ds *buf; // IPC_STAT & IPC_SET
  unsigned short int *array;� // GETALL & SETALL
};

/*
* Modify the data structure for semaphore
* @param: id: descriptor
* @param: nrSem: index of semaphore in the set
* @param: cmd: what operation to select
* @return: -1 error, 0 or positive val (depending on cmd)
*/
int semctl(int id, int nrSem, int cmd, union semun parametru);
```

|CMD Values||
|-|-|
|IPC_STAT|work with set|
|IPC_SET|work with set|
|IPC_RMID|delete set|
|GETVAL|get val of nrSem|
|SETVAL|set nrSem|
|GETALL|read all set and store in buffer|
|SETALL|modify values for whole set|
|GETNCT|get nr of processes waiting for sem to rise|
|GETZNCNT|get nr processes that wait for sem to become 0|
|GETPID|get pid of process that made last call to semop fun|

## Shell commands
- `ipcs` `ipcm` commands
- ipcs -> ged info about semaphores & other inter process communication means
- ipcrm - delete set of semaphores

