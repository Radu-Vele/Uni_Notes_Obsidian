---
tags: [Notebooks/Java Google]
title: Course 11.04.2022 Exceptions & IO
created: '2022-04-11T16:23:17.416Z'
modified: '2022-04-13T16:12:14.344Z'
---

# Course 11.04.2022 Exceptions & IO

## Exceptions
> Abateri de la modul normal de functionare a programului

Eroare in metoda -> Crearea unui obiect Exception -> Obiectul e trimis la runtime system.

### Exception object
- info about the error
- locul si starea programului unde s-a intamplat
- denumire ***Throwing an exception***

Pathway
- se arunca exceptia si se cauta handler (handler catches exception)

Exception
- checked - recovery is possible
- unchecked - no recovery (Runtime Exceptions) - bugs, logic errors - nu suntem obligati sa le prindem.

```java
catch (IOException ex) {
  logger.log(ex);
  throw ex;
}
```

Finally block
- always called

### Error object
- no recovery 

## Objects to retrieve
- e.printStackTrace()

## Why exceptions?
- separate error code from normal code ish 

```java
//Try with resources
try(Closeable resources) {
  //if exception is thrown the resources are closed
}
```

## I/O
> Stream = data sequence
- Byte stream (citim/scriem bytewise) (FileInputStream)
- Characters (FileReader/FileWriter)
- Buffered Streams - temporarly store I/O data (to avoid many readings from the memory)

### NIO
- advantages

## TODO:
- read Exceptions slides + quiz
- challenges Dessign Pattters + Exceptions (>= 1/2)

## Wrap-up:

