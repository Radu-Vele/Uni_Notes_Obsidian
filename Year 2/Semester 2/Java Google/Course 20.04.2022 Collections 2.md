---
tags: [Notebooks/Java Google]
title: Course 20.04.2022 Collections 2
created: '2022-04-20T15:35:24.861Z'
modified: '2022-04-20T16:25:37.277Z'
---

# Course 20.04.2022 Collections 2

## Sets
- no duplicates
   - HashSet
   - TreeSet
   - LinkedHas

## Maps
- if we have the same key for another value => overwritten value

- there are some methods that apply to all collections

## Equality
a. "==" -> verify references

b. "equals()" -> method overwritten by programmer 
- there are some rules to be followed (reflexive)
- equal objects must have the same hashCode();
- hashCode() added for eficiency of HashMaps

## Ordering
- use Comparator

```java
//met 1
public Comparator byAge = new Comparator<Person>() {
  @Override 
  public int compare(Person p1, Person p2) { //Anonymous class
    return p1.age - p2.age;
  }
}

Collections.sort(list)

//met2 
class implements Comparable...
```

## Wrappers
- unmodifiable collection
- thread-safe collections

## Algorithms
### Sorting 
### Shuffling
### Data manipulation
### Searching
### Composition
### Find extremes
