---
tags: [Notebooks/ECG]
title: Lab 9
created: '2022-04-14T05:21:20.136Z'
modified: '2022-04-14T05:34:38.820Z'
---

# Lab 9

Object coordinates -> 3D Object

- Local coordinates initially for an object =

### Modelling transformation
- scalare, translation, rotation

### Camera transformation
- bring camera to origin, all coordinates are relative to the camera
(multiply 2 matrices with different values)

### Projection
- bring all coord in a canonical view (2D surface)
- we have a near and far plane => canonical view
- $\theta$ is the field of view

### Viewport transformation
- bring from the canonical view to the screen space (translate left up corner to (0, 0) and scale to screen dimension + multiply the y axis with (-1) );

### Perspective divide
- divide all coordinates obtained by a certain value

## TODO:
- projection.h functions.
- the other functions afterwards. 
