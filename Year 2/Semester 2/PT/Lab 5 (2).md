---
tags: [Notebooks/PT]
title: Lab 5
created: '2022-03-17T08:10:07.511Z'
modified: '2022-03-26T14:51:51.733Z'
---

# Lab 5

## Assignment 2
---
What we gotta do:
- Queue <-> Thread
- Client - normal class
- Simulation Manager Thread
- More on presentation from dsrl
- Timer master (like a counter) that sets the global time
- Thread-safe - 2 thread-uri sa nu faca scriere concurenta

- output: current queues, avg waiting time, avg service time, peak hour.

### Flow:
- $t_{arrival} \ge t_{global}$ => Introduce a new client
- for $t_{service}$ the client has to be at service (front of the queue)

### Design pattern:
-

### Classes:
|Name|Attributes|Methods|Mention|
|-|-|-|-|
|Client| ID, $t_{arrival}$, $t_{service}$ ||Randomly generated instances|
|Queue|blockingQueue<Clients\>|void run()|Implements ***Runnable*** class|
|Simulation|||extends Runnable, deals with clients, sends to queue the new |

```
/*
* Running a queue
*/
void run() {
  while(simuRunning) {
    Client c = q.peek(); //i.e. get(0)
    c.decreaseServiceTime();
    if(c.getServiceTime() == 0) {
      q.remove(); //pop queue
      Thread.sleep(1000); //use try catch here
      //putem bloca thread ul si atat timp cat dureaza service time
    }
  }
}
```
```
/*
* Running the simulation
*/
void run() {
  while(simRunning) {
    simTime++; //global sim time
    for(Client c: waitingList) {
      if(c.getArrival >= simTime){ //can use atomic integer time
        Queue q = //coada cu timp minim sum(serviceTime)
        q.add(c);
        waitingList.remove(c);
      } 
    }

    Thread.sleep(1000);

  }
}
```

### GUI:
- Command panel for inputting the simulation parameters (text box)
- Print Queues (maybe with some labels) 
- Putem afisa in panou tot din simulation manager (update each textBox)

### Thread theory:
---
- Better approach -> implement *Runnable* rather than extending Thread
- Use concurrent collections (Blocking Queue)
- there may be a huge number of threads (we shall have 30 'tops)
- solution ***EXECUTOR***

Executor = equivalent to our client management but for threads.

- Return from Run method => implement ***Callable***  

### TODO:
---
1. Implement Classes :white_check_mark:
2. Theory Aspects :white_check_mark:
3. Test random generator :white_check_mark:
4. Run threads :white_check_mark:
5. Generate output txt


### Q's
---
1. When do the threads of the queues start & stop (while(true))? do they know about globalSimTime?
2. GUI with variable number of queues? (separate windows?)
3. DS are ok?
3.1. Queue max size?
4. Should we use the executor?
5. Strategy is ok?
6. Daca ajung mai multi clienti in acelasi timp ii adugam pe toti la momentul respectiv?

