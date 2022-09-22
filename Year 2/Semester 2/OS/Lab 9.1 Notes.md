---
tags: [Notebooks/OS]
title: Lab 9.1 Notes
created: '2022-04-15T09:08:23.400Z'
modified: '2022-05-27T07:09:14.948Z'
---

# Lab 9.1 Notes

Next friday 
- we should recover the lab 
-  checkout poll - wednesday 9:00?
- maybe Asynchronous (?).

## Deadlock
- se mutex uri care se blocheaza reciproc somehow
- daca sunt mai multe mutex uri ele trebuie luate in ordine in aceeasi locatie, like a stack

## Forget to release
- se poate ajunge in deadlock :skull:
- nu uita sa dai unlock inainte de function return

## TODO
- insist pe problema 3 pt assignment :triangular_flag_on_post:
- la pb 1 in cond variable could keep whose thread time is now. (cu una sau mai multe condition variables)
```C
turn = 0 //global variable to be sync as well
while(notMyTurn(Turn, ...)) {
  cond_wait
}

// execute the increment
```

# Lab Exam Code Examples

```c
/**
* How to...
**/

/*
* create, destroy, locs & c_var
*/
    pthread_cond_t condition_var;
    pthread_mutex_t lock;

    pthread_cond_init(&condition_var, NULL);
    pthread_mutex_init(&lock, NULL);

/*
* use a cond var
*/
    int cond;
    int other_cond;

    pthread_mutex_lock(&lock);

    while(!cond) {
        pthread_cond_wait(&condition_var, &lock);
    }

    if(other_cond) {
        cont = 1;
        pthread_cond_signal(cond);
    }

    pthread_mutex_unlock(&lock);

    pthread_mutex_destroy(&lock);
    pthread_cond_destroy(&lock);


```
