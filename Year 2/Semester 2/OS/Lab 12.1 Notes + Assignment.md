---
tags: [Notebooks/OS]
title: Lab 12.1 Notes + Assignment
created: '2022-05-13T09:13:50.557Z'
modified: '2022-05-27T07:52:53.905Z'
---

# Lab 12.1 Notes + Assignment

## Colocviu:
- Probabil: 2-3 probleme pe calculatoarele de aici, closed book

- similare cu problemele din Guidance

- probleme cu subpuncte diferite

***Topics***: 

-> File System (open, read, write, seek, dir...). 

-> Processes, Threads, Synchronization (mutex, cv, sem, fork, wait, join).

-> Inter process communication (pipes, fifo, shared memory).

# Assignment
- use named pipes (rendez-vous pipe at creation)

```c
mkfifo("name");

P1() {
  open("name", O_READ);
}

P2() {
  open("name", O_WRITE);
}
```

La noi in assignment

- testerul creeaza procesul nost P1

- comunicare simpla full-duplex --> create 2 pipes:
1. response pipe (P1 calls mkfifo("RESPONSE"))
2. request pipe (P1 calls open("REQUEST", O_READ))

Careful about the order of calling open for READ and WRITE (alternative) 

```c
P1() {
  mkfifo("REQUEST");
  open("REQUEST", O_WRITE);
  open("RESPONSE", O_READ);
}

P1() {
  mkfifo("RESPONSE");
  open("REQUEST", O_READ);
  open("RESPONE", O_WRITE);
}
```

## Communication protocol

- idee: create functions SEND_STRING, SEND_INT, RECEIVE_STRING, RECEIVE_INT; (useful to avoid writing multiple steps in more parts of the program);

- careful about the return messages

- 2.9. more complicado :alien: 
- SF file is inspired from Windows Portable Executable files

# Lab Exam Code Examples

```c
/**
* How to...
**/

/*
* Create shared memory object
*/
    int fd = shm_open("/myMem", O_RDWR | O_CREAT, 0666);

    void* access = mmap(NULL, 1024, PROT_READ | PROT_EXEC, MAP_SHARED, fd, 0); //Needs to be mapped also

/*
* Read/Write from shared mem object
*/

    access = (char*)access + 20;

    *(unsigned*)access = 12; 

    unsigned read_nr = *(unsigned*)((char*) access + 30)

    munmap(access, 1024);

    shm_unlink(fd);

/*
* Map file to memory
*/
    char path[20];
    in fd = open(path, O_RDWR);

    void* access = mmap(NULL, size, PROT_EXEC | PROT_READ, MAP_SHARED, fd, 0);

    munmap(access, size); //unmap file

    unlink(path);//get rid of file

/*
* Read/Write to mapped file area
*/
    //just access the pointer to the shared memory area

```
