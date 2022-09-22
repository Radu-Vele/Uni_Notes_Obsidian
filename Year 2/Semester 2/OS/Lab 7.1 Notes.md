---
tags: [Notebooks/OS]
title: Lab 7.1 Notes
created: '2022-04-01T09:07:46.094Z'
modified: '2022-05-27T07:15:15.242Z'
---

# Lab 7.1 Notes

## Concurrency and Parallelism
### :a: Concurrency
> Se refera la o competitie pentru o resursa (CPU).

e.g. syncAndWait in javascript

### :b: Parallelism
> Doua chestii se intampla in acelasi timp (fizic) independent una de cealalta

- we can have concurrency without parallelism

### :heavy_exclamation_mark: Remark: 
Paralelismul determina impartirea timpului de rulare la numarul de fire de executie. (in limita resurselor).

---
### When to use threads?
- problema cu multe date si putem lucra pe ele independent in paralel (impartirea a data set-ului pe portiuni)

e.g. : nu putem face divide et impera cu thread-uri though

- context: HDD e cea mai slow componenta din calculator. Asteptare "lunga" pentru anumite operatii => las un thread in urma sa astepte pentru date si introduc alt thread care face altceva.
  - threads are an abstraction for a CPU ish (fir de executie)

> Threads vs Processes: procesele sunt izolate (de la fork incolo sunt complet independente), thread-urile exista in contextul aceluiasi context (daca unul schimba o variabila, le afecteaza si pe celelalte).

## TODO:
2. example la clasa 
3. alege mai degraba variant 1
- la numerele prime nu prea ajuta sa avem paralelism (not a good answer)
- impartire mai ok a unui array: daca avem 4 thread-uri fiecare thread poate sa ia elemente % thread_id

```C
array[nr_threads * i + id];  //face selectia pt un t
```

## Tips & Threa(th)ds:
- daca schimb o variabila, o sa se schimbe in toate thread-urile

# Lab Exam Code Examples

```C
/**
 * How to...
 **/

 /**
 * Create N threads & pass arg structure
 **/
    int N = 50;
    pthread_t th[N + 1];
    struct args* arguments[N + 1];

    // Create threads
    for(int i = 0; i < N; i++){
        arguments[i].id = i + 1;
        int ret = pthread_create(&th[i], NULL, (void* (*) (void*))rescued_person, &th_args[i]);

        if(ret != 0) {
            printf("FAIL");
        }
    }

 /**
 * Wait for the threads
 **/

    for(int i = 0; i < N; i++) {
        pthread_join(th[i], NULL); //if I want a returned value pass it in the arguments structure as pointer
    }

/*
* Parallelize an operation
*/

    //product of first M numbers:
    //create an array of partial products
    //for each thread think where to start and to end in the array

```
