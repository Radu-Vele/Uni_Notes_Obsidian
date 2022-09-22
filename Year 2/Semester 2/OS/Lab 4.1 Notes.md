---
tags: [Notebooks/OS]
title: Lab 4.1 Notes
created: '2022-03-11T10:05:27.251Z'
modified: '2022-05-27T06:15:00.104Z'
---

# Lab 4.1 Notes

## Assignment 1
- de făcut primul test cu variant to work (vedem dacă merge python-ul pe VM) ASAP
- need next lab (5) to solve all of the assignment

## Lab themes 4 & 5
- How to use API Linux

## Lab 4

### 1. Files
---
- bazele o fost puse cand lucram in C
```
/*
* High level functions from the platform-independent C library
* Apeleaza functiile platform-dependent (OPEN, CLOSE)
*/ 
fopen();
fclose();
```

### **FILE** = Abstraction used to organize the data in the memory.  
- dummy mistake: suprascriere a fisierelor gresite

Permisiuni in linux:



### 1.1. OPEN
---

- returneaza un descriptor i.e. integer associated to an open file
- **KERNEL** -> are logica sistemului de operare (nu poate fi accesat de user in mod direct) - highest privilege level.
- ***Descriptor*** = like a token associated to the file - used to access the file resource

### 1.2 READ
---
Remark: returneaza cat o citit efectiv (maybe less decat cat i-am dat noi)
- error: ret -1;
- Write works in a similar way

### 1.3 CLOSE
---
- give back token



### 2. Permissions

grup -> ce permisiuni *rwo*

- 3 biti, fiecare numar din bitstring inseamna daca ai permisiune pentru acea operatie

|R|W|X|
|--|--|--|
|1|1|1|
|1|0|1|

### Tips
---
- carte Linux -> aprofundare concepts (The Linux Programming Interface)
- *avoid reading and writing by one character (ne-ar da timeout cand programul ii testat)*
- install "Everything" - gaseste instant orice fisier pe disk.

### Lab Activity
---
- consider bit and little Endian: numarul are bytes-ii inversati 
- extensia VSCode - HexEditor  sau ImHex app
- nu facem presupuneri legate de mărimea fișierului   (e.g. citim doar pe bucatele)

# Lab Exam Code Examples

```c
/**
* How to...
**/

/*
* Check if a path corresponds to a file
*/

    int fd;
    char path[20];
    fd = open(path, O_RDWR);
    if(fd < 0) {
        printf("Not a file");
    }

    //Alternative

    struct stat file_status;
    stat(path, &file_status);

    if(!S_ISREG(file_status.st_mode)) {
        printf("Not a file");
    }


/*
* Check if a path corresponds to a directory
*/
    DIR* dir;
    stat(path, &file_status);

    if(!(S_ISDIR(file_status.st_mode))) {
        printf("Not a dir");
    }

    //Or

    dir = opendir(path);
    if(dir == NULL) {
        printf("Not a dir");
    }


/*
* Create a new file in a directory
*/

    // dir = pointer to dir

    sprintf(path, "%s/new_file.txt", path); //create path
    int fd = open(path, O_CREAT | O_RDWR, 0600);

    if(fd < 0) {
        printf("Cannot create file");
    }
    


/*
* Iterate a directory
*/

    struct dirent* curr_entry;

    while(curr_entry != NULL) {
        curr_entry = readdir(dir);
    }

    closedir(dir);

/*
* Get information about a file 
*/

    struct stat file_stat;
    lstat(path, &file_stat);

    //important
        mode_t mode = file_stat.st_mode; //find out if file/dir/fifo/ permissions using S_IRUSR

        /**
         * struct stat {

            mode_t st_mode; /* file type & rights 
            ino_t st_ino; /* i-node 
            dev_t st_dev; /* număr de dispozitiv (SF) 
            nlink_t st_nlink; /* nr of links 
            uid_t st_uid;  /* owner ID 
            gid_t st_gid;  /* group ID
            off_t st_size;  /* ordinary file size 
            time_t st_atime;  /* last time it was accessed 
            time_t st_mtime;  /* last time it was modified 
            time_t st_ctime;  /* last time settings were changed 
            dev_t st_rdev; /* nr. dispozitiv */
            /* pt. fişiere speciale /
            long st_blksize; /* optimal size of the I/O block 
            long st_blocks;  /* nr of 512 byte blocks allocated 
        **/

/*
* Read line by line
*/

    //read in buffer
    char buff[256];
    while(read(fd, &buff, 256) == 256) { //can also verify that read >= 0 so we can read even less in the buffer

        char line[256];
        int j = 0;

        for(int i = 0; i < 256; i++) {
            if(buff[i] == '\n') {
                //line is a finished line
                j = 0;
            }
            else {
                line[j] = buff[i];
                j++;
            }
        }
    }
```






