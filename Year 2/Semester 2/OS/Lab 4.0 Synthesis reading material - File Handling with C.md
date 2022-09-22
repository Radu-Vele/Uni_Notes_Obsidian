---
tags: [Notebooks/OS]
title: Lab 4.0 Synthesis reading material - File Handling with C
created: '2022-03-10T12:38:32.562Z'
modified: '2022-03-18T10:22:42.932Z'
---

# Lab 4.0 Synthesis reading material - File Handling with C

## 1. File Descriptors
- open file <-> descriptor (int > 0) 
- Standard file descriptors:

| Descriptor | Meaning |
|-----------|--------|
|0  |stdin  |
|1  |stdout |
|2  |stderr |

- calls that generate descriptors: create, open, fcntl, dup, pipe

## 2. System calls

### 2.1 OPEN
- open/create file 

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>

int open(const char *path,
        int flags,... /* mode_t mod */); //returns file descriptors
```

- 3 param => create, 2 param => open
- the descriptor returned can be used in other sys calls
- => pointer file to the first byte
- access rights defined in sys/stat.h
.
- FLAG-uri interesante
    - O_RDWR - read & write
    - O_CREAT - daca fisierul 

|No.|Case|Exists|Not exists|
|--|---|----|--|
|1.|Create a new file|no O_EXCL => fails|
|2.|Open existing||no O_CREAT => fail|
|3. |Don't care 

### 2.2 CREAT

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>

/*
* @Param: path - file name
*        mod - access rights
*/

int creat(const char *path, mode_t mod); 

//Equivalent OPEN call:
open(path, O_WRONLY | O_CREAT | O_TRUNC, mod);

```
- returned descriptor 
- initial size = 0

### 2.3 READ
```
#include <unistd.h>

/*
* @Param: noct = nr bytes read 
*        fd = source file descriptor
*        buf = destination buffer
*/
ssize_t read(int fd, void* buf, size_t noct);
```
- read from current position.
- current position pointer automatically incremented

### 2.4 WRITE

```
#include <unistd.h>

/*
* @Param: noct - nr bytes written
*        fd - current file descriptor
*        buf - source of the written content
*/
ssize_t write(int fd, const void* buf, size_t noct);
```
- Remark: writing onto the disk is delayed => cache buffers are used

### 2.5 CLOSE
- eliminate descriptor
```
#include <unistd.h>
int close(int fd)
```

### 2.6 LSEEK
```
#include <sys/types.h>
#include <unistd.h>
/*
* @Param: fd -descriptor
*         offset - distance to the position
*         ref - SEEK_SET, SEEK_CUR, SEEK_END
*/
off_t lseek(int fd, off_t offset, int ref);
```
- position pointer to another area
- ref $\in$ {SEEK\_CUR,SEEK\_SET, SEEK\_END\}
.

|MSB|8|7|6|5|4|3|2|1|LSB|
|-|-|-|-|-|-|-|-|-|-|-|
|Seek_ptr (read 1)| Seek_ptr (read 2 vals)

```
seek(0, SET); //move to start
seek(0, END); //move to end + returns the size of the file
seek(0, CUR); //no move + returns current position in file
```
Util la Assignment 1

### 2.7 LINK & UNLINK
- link/unlink file to a directory 

***LINKS*** 
- we know that files are represented as I-nodes
Two types: **symbolic** (se refera la un fisier existent), *hardlink* (cloneaza fisierul, like shortcuts-ish)

```
//LINK

#include <unistd.h>

int link(const char* oldpath, const char* newpath);
int symlink(const char* oldpath, const char* newpath);

//UNLINK //the counter of links is decremented => at 0 the file is erased
#include <unistd.h>
int unlink(const char* path);
```

### 2.8 STAT, LSTAT, FSTAT
- Obtain information about a file / link
- ls uses this function
- generate a vulnerability -> ne dau un snapshot despre files la un anumit timp, dar fisierul se poate schimba.

|Function| Meaning|
|-----|----|
|stat| information from the i-node returned in buffer|
|fstat|similar but works with files that have already been opened (known descriptor)|
|lstat|difers from stat regarding the symbolic links|

### 2.9 ACCESS
```
#include <unistd.h>
int access(const char* path, int mod);
```
- verifies access right

### 2.10 UMASK
```
#include <sys/types.h>
#include <sys/stat.h>

mode_t umask(mode_t mask);
```
- returns the previous mask (description of the access rights of the file ish)

### 2.11 CHMOD
- change access rights
- change owner and group => can use **CHOWN** for only that 
```
#include <sys/types.h>
#include <sys/stat.h>

int chmod(const char* path, mode_t mod);
```

### 2.12 UTIME
- gives information about access time (more in the .html file)
.
.
.


## 3. Functions to work with directories
```mermaid
graph LR
kernel --> dir[writing a directory]
```
- Dir structure -> sequence of entries
- used in homework.

Directory represented as a File: *Everything is a file in Linux*

```
/*
* Reading the directory entries
*/

#include <sys/types.h>
#include <dirent.h>

DIR* opendir(const char* pathname); //open directory, NULL if failed

struct dirent* readdir(DIR* dp); //function that reads an entry at each call 

void rewinddir(DIR* dp); //reposition file pointer to first dir entry

int closedir(DIR* dp); // close opened dir
```
```
struct dirent {
ino_t d_fileno;  // i-node nr.
char d_name[MAXNAMLEN + 1];// file name

}
```
- opendir -> returns a handle / directory descriptor
  

