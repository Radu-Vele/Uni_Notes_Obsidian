---
tags: [Notebooks/Java Google]
title: "Course 09.05.2022 Reactive \U0001F4A0"
created: '2022-05-04T17:03:54.206Z'
modified: '2022-05-22T12:01:24.494Z'
---

# Course 09.05.2022 Reactive :diamond_shape_with_a_dot_inside:

> A way of designing an application

Responsive, Resilient, Elastic, Message-Driven

## Programming paradigms
### 1. Imperative.

- many Statements
- hard to maintain

### 2. Structured
- use control flow with for, while, ...
instead of only statements

### 3. Procedural
- use functions
- side effects

### 4. Functional
- eval expression only based on input, no side effects.
- lazy evaluation (executed only when needed)
- iterate through recursion
- parallel execution
- pure functions can't do some stuff: database access, email sending, network access, print files

### 5. Declarative
- don't specify control flow, only declare structure

---

### a. Asynchronous
- refers to parallel programming (run some parts of the program without affecting the others)
- for multi-core CPU
- total time = longest operation time

### b. Reactive
- refers to the behavior changes w.r.t events that occur;
- the code is designed by spliting the exec. into small steps such that they can be executed in parallel

### c. Object-Oriented
- encapsulation, message passing, dynamic binding

---

# Reactive Streams
- uses Push-Subscribe framework

### Publisher
- emit data
- subscribe()

### Subscriber
- deals with subscribing / consuming data

### Subscription
- controls the message between Publisher and Subscriber
```
request();
cancel();
```

### Processor
- between subscriber and publisher

## Reactive features

### BackPressure
- consumer is able to signal to many emissions

### Error-Handling
- the original sequence is not allowed to continue by the *error_handling_operators*

  - onErrorReturn
  - onErrorResume
  - onErrorMap
  - doOnError
  - doFinally

- can also retry (resubscribe)

### Non-blocking

### Threading and scheduler
- if we don't specify else, the source runs in the Thread in which subscribe() call was made

- determine where to run thread : immediat(), single(), elastic(), .parallel()
.publishOn() -
.subscribeOn()


# ReactiveX
- asynchronous programming with reactive stream
- Observer + Iterator

- several operators change the Publisher until it gets to Subscriber (that's also when all operations happen)

# Implementation
RxJava,
Reactor,
Akka Streams

