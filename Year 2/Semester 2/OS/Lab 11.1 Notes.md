---
tags: [Notebooks/OS]
title: Lab 11.1 Notes
created: '2022-05-06T09:10:55.019Z'
modified: '2022-05-27T07:23:03.381Z'
---

# Lab 11.1 Notes

- Pipe is based on producer - consumer pattern:
  - i.e. a circular queue
  - meanwhile reader-writer: makes it more efficient to have more reads than writes
  - rendezvous is only about opening a pipe

- the communication through the pipe is done as a bytestream (the need for a communication protocol)

:star: Assignment
- e.g. to know when to stop reading - introduci un 0.(daca datele nu contin delimitatorii) / lungime fixa / header with length specified before

|len|***message***|len|***message***|len|***message***|len|***message***|
|-|-|-|-|-|-|-|-|

- nu intra sockets la colocviu

## TODO
1. Alternative execution
Bonus: 
Sockets - un punct la examen

# Lab Exam Code Examples

```c
/**
 * 
 * How to...
 **/



 /*
 * create named pipes /anonymous
 */

    //anonymous -- communication 
    int fd[2];
    pipe(fd); //fd[0] - read fd[1] -write

    close(fd[0]) //use fd only for writing;

    //named
    
    mkfifo("./pipe", 0666);

    int fd_fifo = open("./pipe", O_RDWR);


 /*
 * Read / Write
 */

    //anonymous

    read(fd[0], &read_bytes, 10);

    //named

    read(fd_fifo, &read_bytes, sizeof(char));

    close(fd);
    clode(fd_fifo);


    write//similar
 /*
 * Avoid probems
 */

    //Dont read from pipe that is not open for writing by another process
    //Dont write to pipe that is not open for reading by another process

```
