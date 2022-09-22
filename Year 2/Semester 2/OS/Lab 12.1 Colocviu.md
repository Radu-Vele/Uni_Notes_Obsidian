---
tags: [Notebooks/ECG]
title: Lab 12.1 Colocviu
created: '2022-05-25T07:03:59.800Z'
modified: '2022-05-25T21:22:10.942Z'
---

# Lab 12.1 Colocviu

## Colocviu 2021

(*) to test

|Grila| Answer| Explanations|
|-|-|-|
|1| b|cross product obeys the right handed rule (regula burghiului drept)|
|2|
|3| ***| z buffer 
|4| a | potentially leaving point (pag 19)
|5 |a| pag 39.
|* 6| f | -inf (in the lab)
|7|a | inverse order of operations|
|8|b |
|9| a | sunt intersectii doar pe prelungirile edge-urilor clipping window
|10| b | 0.0 / 0.0 is NaN
|11| d | cross product right hand rule
|*12| c, a| after the algorithm finds P2 (0001), and P3 (0100), then simple rejection
|13 | b| matrix dot product
|14| b| pag 20|
|15| ? | maybe perspective projection
|16| code below|
|17| b | it has to be moved to origin, transformed, moved back (rotation & scaling is done relative to the origin) (pag 12) |
|18| f | there is a bounding box that contains the triangle
|20|b, c| b - true if there is anything inside the window, c - the points are 'cut' on the intersection with the edges and prelungirile lor
|21| a| scale by 1 / value (pag 13)
|22| a| the classification is done using the dot product between Normal vector of edge (exiting) and (P1 - P0) <= we need the angle
|23| f | Right ( x > x_max) Up (y > y_max) Left (x < x_min) Down (y < y_min)
|24| b| inverse translation - value (pag. 12)
|25| a, f, g | see bresenham.cpp
|26| b | pag 38
|27| c | inverse order of operations
|28| c | inverse order of operations
|29| a | right hand rule|
|30| c, d| right hand rule multiple times :dizzy:| 


## Additional

```cpp
/************************************
* Grila 8 - Multiply Two Matrices
*************************************/
mat3 mat3::operator *(const mat3& srcMatrix) const {
		mat3 result = mat3();

		for (int i = 0; i < 3; i++) {
			for (int j = 0; j < 3; j++) {
				
				float res = 0;

				for (int k = 0; k < 3; k++) {
					res += this->at(i, k) * srcMatrix.at(k, j);
				}

				result.at(i, j) = res;

			}
		}
		return result;
	}


/***********************************
* Code for rotating a rectangle
***********************************/
{
  diag_intersection.x = (P1.x + P1.y) / 2;
  diag_intersection.y = (P1.y + P2.y) / 2;
  final_matrix = translate(-diag_intersection.x, -diag_intersection.y);
  final_matrix = final_matrix * rotate(10);
  final_matrix = final_matrix * translate(diag_intersection.x, diag_intersection.y);
  P2 = final_matrix * P2;
  P1 = final_matrix * P1;
}

/**************************************
* Code for drawing line in the fifth octant Bresenham
*
*
*****************************************/
{
case 5:
      tmpStartX = tmpCurrentX = line.startX;
      tmpEndX = line.endX;
      tmpStartY = tmpCurrentY = line.startY;
      tmpEndY = line.endY;

      d = 2 * dx - dx;
      inc1 = 2 * dy;
      inc2 = 2 * (dy - dx);

      while (tmpCurrentX > tmpEndX)
      {
        //Draw current point
        SDL_RenderDrawPoint(renderer, tmpCurrentX, tmpCurrentY);
        --tmpCurrentX;

        if (d < 0)
          d += inc1;
        else
        {
          d += inc2;
          ++tmpCurrentY;
        }
      }
    break;
}
```

## TODO:
- Understand algorithms:
1. Cyrus Beck
  - entering point (angle normal - line is gt 90 deg) -> take the max 
  - leaving point (angle lt 90 deg) -> take the min
  - grije la ordinea de parcurgere

2. Cohen Sutherland
  - codes computation
  - how are points taken
  - simple rejection code1 AND code2 have a component equal to 1
  
3. Bresenham
  - 8 octants
  - code similar ish (compute increments, increment/decrement)
  - pentru code, daca suntem in octantii 2 3 sau 6 7 incrementam in while y-ul si in if x-ul, altfel invers
  - m < 1 (sub 45deg), m > 1 (peste 45deg)
  - atentie ca y-ul creste in jos 

4. Viewport

 - Order of transformations: model * projection * camera
 - normal vector to triangle (burghiu drept) (B - A means: A------>B)

5. Zbuffer

> The final pixel is updated only if the candidate pixel is closer to
the center of projection than the value already in the buffer. If the pixel is updated, the existing depth
value in the z-buffer is replaced by the new pixel’s depth.

6. Bezier

7. Barycentric coordinates
- points computed in bounding box
- if(0 < alpha < 1 and 0 < beta < 1 and 0 < gamma < 1) the point is inside triangle
- on edge if one barycentric is 0, vertex if two barycentric are 0


## Remarks
- dot product
len1 len2 cos
- cross product
len1 len2 sin
