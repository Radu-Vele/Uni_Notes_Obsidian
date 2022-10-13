# My plan

>[!Important] If possible try to do 2 lectures per week 
>- Ocasionally run git pull
>- Do labs when they are linked to the required lectures already visited

## Tracking

### Lectures
- [x] AI1_01 
	- Defining AI, Talking about implications
- [x] AI1_02
	- Vectors and Matrices using **Pandas**, **Numpy** (for scikit library)

	Cool stuff: Numpy reshape function

	- Tensors - have any number of dimensions $\Rightarrow$ the **RANK** of the tensor   

	Scalar addition and multiplication go **elementwise**

	Matrix addition and **Hadamard Product** are defined **elementwise** as well. The Hadamard Product is the default in Numpy
	$$\begin{bmatrix}
	2 & 3\\
	2 & 0
	\end{bmatrix}
	*
	\begin{bmatrix}
	1 & 2\\
	3 & 0
	\end{bmatrix}
	= 
	\begin{bmatrix}
	2 & 6 \\
	6 & 0
	\end{bmatrix}
  $$

	```Python
	# Matrix multiplication
	np.dot(A, B)

	#identity matrices
	np.identity(3)

	#inverses
	import numpy.linalg as npla
	npla.inv(A)
	#Moore-Penrose pseudo-inverse
	npla.pinv(A)
	```

	Numpy **Universal functions** (applied piecewise)

	**Vectorization** - use fast array operators instead of loops
		- can use %timeit to get the execution time
- [ ] AI1_03
- [ ] AI1_04
- [ ] AI1_05
- [ ] AI1_06
- [ ] AI1_07
- [ ] AI1_08
- [ ] AI1_09
- [ ] AI1_10
- [ ] AI1_11
- [ ] AI1_12
- [ ] AI1_13
- [ ] AI1_14
- [ ] AI1_15
- [ ] AI1_16
- [ ] AI1_17
- [ ] AI1_18
- [ ] AI1_19
- [ ] AI1_20
- [ ] AI1_21
- [ ] AI1_22
- [ ] AI1_23

### Labs

- [x] AI1_01
	- basic numpy operations, not big deal
- [ ] AI1_02 Pandas
- [ ] AI1_03
- [ ] AI1_04
- [ ] AI1_05

