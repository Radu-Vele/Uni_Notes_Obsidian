---
tags: [Notebooks/ECG]
title: Lab 7 Cyrus-Beck Clipping Algorithm
created: '2022-03-31T05:16:00.515Z'
modified: '2022-05-25T12:34:25.136Z'
---

# Lab 7 Cyrus-Beck Clipping Algorithm

### Line parametric equation:

$P = (1 - t) * P1 + t * P2$

1) t = 0 => P = P1
2) t = 1 => P = P2

>t could be tought of as a "percentage"

How to work with it? 
- Apply the formula to both coordinates: P.x, P.y;

Negative t? 
- get a point to the left of the initial point

$t > 1$
- point on the right extension of the line

## Cyrus-Beck

- relies on the t parameter to find intersections between the line and each clipping edge
- Idea:
  - given the window -> a set of clipping edges.
  - each edge has a normal vector associated to it.

  1. Given a line P0, P1 we want to compute the t parameter(s) of the line where it intersects the window clipping edges (for all window clipping edges)
  
  2. Partition the intersection points into the "left" (*entering*) and "right" (*leaving*) -> determined using the angle between line and normal to each edge

 $angle > 90 deg$ => entering
  $angle < 90 deg$ => leaving

  3. If t is entering, make sure that I choose the *maximum* of its value and the previous $t_{entering}$ . If t is leaving, choose the minimum $t_{leaving}$

  4. Plug in the two t values obtained. Draw a line between the two.

- challenges: how to input the normals given the corners?
  - compute vector that is a clipping edge, the normal could be computed using:
    1. Cross product => between the Oz axis and the edge vector and normalize it. (order: Z, Edge).
    2. Rotate vector by $90 \degree$
      ----------------> X
      |
      |
      |
      |
      |
      _ y

  - compute the intersection points - formula in slides
  $P_{E_{i}}$ is (we choose it to be) the first point of the clipping edge
  
  $t= \frac{N_{i}\cdot(P_{0} - P_{E_{i}})}{-N_{i} \cdot D}$
  
  - therefore we need to compute the $P_{E_{i}}$ for each edge

- weak points: daca linia pe care vrem s-o clip-uim e paralela cu un clipping edge :worried:

- algorithm in lab resources
