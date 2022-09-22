---
tags: [Notebooks/ECG]
title: Lab 6
created: '2022-03-24T06:14:55.396Z'
modified: '2022-05-25T13:34:18.121Z'
---

# Lab 6

## Clipping Algorithm

***Cohen Sutherland***
- avem o fereastra patrata pe care o suprapunem peste elem grafice
$x_{rectan_{min}} \le x_{points} \le x_{rectan_{max}}$
- explicatie pe xOy

dar in sdl*
O
-----------> x
|
|
|
|
^ y

2 cases
1. trivially accepted (AB) - line entirely into the window
2. trivially rejected (line entirely outside window and in the same side w.r.t. window)

## Encoding

|1|1|1|1|
|-|-|-|-|
Up|Down|Right|Left

```c
// Algorithm
/*
* Why we need that?
* - enhance program performance by focusing only on one area
* - x_min, x_max, y_min, y_max limits of rectangular window
* - rectangles around windows encoded on 4 bits
* - bits: up_down_right_left e.g.: 1001 (up left), 0000 (our window including edges)
*/

repeat until FINISHED = TRUE {
  COD1 = computeCScode(x1, y1) //compute the 4 digits code for P(x1, y1)
  COD2 = computeCScode(x2, y2) // compute the 4 digits code for P(x2, y2)
  RESPINS = SimpleRejection(COD1, COD2) //test for simple rejection case

  if RESPINS = TRUE
     FINISHED = TRUE
  else {
    DISPLAY = SimpleAcceptance(COD1, COD2) //test for simple acceptance case

    if DISPLAY = TRUE
      FINISHED = true
    else {

      if(P(x1, y1) is inside the display area)
        invert(x1,y1,x2,y2,COD1,COD2) //if P(x1, y1) is inside the display area, invert P(x1, y1) and P(x2, y2) together with their 4 digits CS codes

      if(COD1[1] = 1) and (y2 <> y1) //eliminate the segment above the display area {
        x1 = x1+(x2-x1)*(Ymax-y1)/(y2-y1)
        y1 = Ymax
      }
      elseif(COD1[2] = 1) and (y2 <> y1) //eliminate the segment under the display area
      {
        x1 = x1+(x2-x1)*(Ymin-y1)/(y2-y1)
        y1 = Ymin
      }
      elseif(COD1[3] = 1) and (x2 <> x1) //eliminate the segment on the right of the display area
      {
        y1 = y1+(y2-y1)*(Xmax-x1)/(x2-x1)
        x1 = Xmax
      }
      elseif(COD1[4] = 1) and (x2 <> x1) //eliminate the segment on the left of the display area
      {
        y1 = y1+(y2-y1)*(Xmin-x1)/(x2-x1)
        x1 = Xmin
      }
    }
  
}
```

## TODO:
- moodle resources
- 
