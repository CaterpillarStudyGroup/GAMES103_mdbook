
P2
## Vectors

P3
## Vector: Definition    


An (Euclidean) vector: *A geometric entity endowed with magnitude and direction*.

$$
\mathbf{P} =\begin{bmatrix}
 p_x\\\\ 
 p_y\\\\ 
p_z\\\\
\end{bmatrix}\in \mathbf{R} ^3
$$


$$
\mathbf{o} =\begin{bmatrix}
 0\\\\ 
 0\\\\ 
0\\\\
\end{bmatrix}
$$

The vector **p** is defined with respect to the origin **o**.

![](./assets/02-2.PNG)     




P4
## Vector: Definition  


The choice of a right-hand or left-hand system is largely due to:    
**the convention of the screen space**.    

![](./assets/02-3.PNG)    


P5
## Vector: Definition  


Vectors can be stacked up to form a high-dimensional vector, commonly used for describing the state of an object.     

![](./assets/02-4-1.PNG)    



Not a geometric vector,but a **stacked vector**.    


P6
## Vector Arithematic: Addition and Subtraction     


$$
\mathbf{p\pm q=} \begin{bmatrix}
 p_x\pm q_x\\\\
 p_y\pm q_y\\\\
p_z\pm q_z\\\\
\end{bmatrix}
$$

$$
\mathbf{p+q=q+p} 
$$
![](./assets/02-5.PNG)    




P7
## Example 1: Linear Representation     



A (geometric) vector can represent a position, a velocity, a force, or a line/ray/segment.    

![](./assets/02-6.PNG)    
![](./assets/02-7.PNG)    



P8
## Vector Norm   


A vector norm measures the magnitude of a vector: its length. 

![](./assets/02-8.PNG)




P9
## Vector Norm: Usage  


![](./assets/02-09.PNG)   

$$
\mathbf{||q-p||} 
$$

> Distance between **q** and **p**    

$$
\mathbf{||p||} =1
$$

> A unit vector


$$
\mathbf{\bar{p} =p/||p||} 
$$

> Normalization as





P10
## Vector Arithematic: Dot Product     


A dot product, also called inner product, is:




$$
\begin{array}{c} 
  \mathbf{p\cdot q}=p_xq_x+p_yq_y+p_zq_z=\mathbf{p^Tq}   \\ \\
 =||\mathbf{p} ||||\mathbf{q} ||\cos \theta 
\end{array}
$$


![](./assets/02-11-1.PNG)   

> Geometric Meanings    


 - \\(\mathbf{p\cdot q=q\cdot p} \\)    
 - \\(\mathbf{p\cdot (q+r)=p\cdot q+p\cdot r} \\)    
 - \\(\mathbf{p \cdot p = ||p||^2_2} \\), a different way to write norm.     
 - If\\(\mathbf{p·q} = 0\\)and \\(\mathbf{p,q}\ne 0\\)then \\(\cos \theta =0\\),then \\(\mathbf{p} and \\(\mathbf{q}\\) are orthogonal.    


P11
## Example 2: Particle-Line Projection


![](./assets/02-12-1.PNG)



P12
## Example 3: Plane Representation     

![](./assets/02-13-1.PNG)


$$
s= \mathbf{(p−c)^Tn } \left\{\begin{matrix}> 0
  & \mathrm{Above the plane} \\\\
 = 0 & \mathrm{On the plane} \\\\
 < 0 & \mathrm{Below the plane} 
\end{matrix}\right.
$$

S: The <u>signed</u> distance to the plane     


Quiz: How to test if a point is within a box?    

![](./assets/02-14-1.PNG)


P13
## Example 4: Particle-Sphere Collision    

![](./assets/02-15.PNG)


If collision does happen, then:

$$
||\mathbf p(t) - \mathbf{c}||^2= r^2
$$

$$
(\mathbf p-\mathbf c+t\mathbf v)·(\mathbf p-\mathbf c +t\mathbf v) =r^2
$$

$$
(\mathbf v·\mathbf v)t^2+2(\mathbf p-\mathbf c)·\mathbf vt+ (\mathbf p-\mathbf c)·(\mathbf p-\mathbf c)-r^2=0
$$


 - Three possiblities:    
    - No root、无碰撞    
    - One root、擦边 if t > 0   
    - Two roots:自碰撞 if t > 0    




P14
## Vector Arithematic: Cross Product


![](./assets/02-17.PNG)


The result of a cross product is a vector:

$$
\mathbf{r=p\times q} =\begin{bmatrix}
p_yq_z-p_zq_y \\\\
 p_zq_x-p_xq_z\\\\
p_xq_y-p_yq_x\\\\
\end{bmatrix}
$$


 - \\(\mathbf r·\mathbf p = 0; \mathbf r·\mathbf q = 0; ||\mathbf r|| = ||\mathbf p||||\mathbf q||   \sin 0\\)                      
 - \\(\mathbf p\times \mathbf q =-\mathbf q\times \mathbf p\\)
 - \\(\mathbf p\times (\mathbf q +\mathbf r) = \mathbf p\times \mathbf q +\mathbf p\times \mathbf r\\)   
 - \\(If \mathbf p \times  \mathbf q =\mathbf 0 and \mathbf p,\mathbf q\ne 0 then \sin =0,then \mathbf p and \mathbf q \\) are parallel (in the same or opposite direction)      


P15
## Example 5: Triangle Normal and Area   


![](./assets/02-18.PNG)


 - Cross product gives both the normal and the area.    
 - The normal depends on the triangle index order, also known as topological order.      


P16
Quiz: How to test if three points are on the same line (co-linear)?     


P17
## Example 6: Triangle Inside/Outside Test    


![](./assets/02-19-1.PNG)

> lf **p** is inside of \\(\mathbf{x_ox_1} \\), then:\\(\mathbf{(x_o - p)\times (x_1 -p)\cdot n >0 } \\)   


![](./assets/02-19-2.PNG)

> lf **p** is inside of \\(\mathbf{x_ox_1} \\), then:\\(\mathbf{(x_o - p)\times (x_1 -p)\cdot n < 0 } \\)    


P18
## Example 6: Triangle Inside/Outside Test


![](./assets/02-20-1.PNG)

$$
\left.\begin{matrix}
\mathbf{(x_0-p)\times (x_1-p)\cdot n> 0}  \\\\ 
\mathbf{(x_1-p)\times (x_2-p)\cdot n> 0}  \\\\ 
\mathbf{(x_2-p)\times (x_0-p)\cdot n> 0} \\\\
\end{matrix}\right\}
$$
Inside of triangle Otherwise, outside.   


\\(\left.\begin{matrix}\mathbf{(x_0-p)\times (x_1-p)\cdot n> 0} 
 \\\\ \mathbf{(x_1-p)\times (x_2-p)\cdot n> 0} 
 \\\\ \mathbf{(x_2-p)\times (x_0-p)\cdot n> 0} 
\end{matrix}\right\}\\) Inside of triangle Otherwise, outside.  






## xample 7: Barycentric Coordinates

![](./assets/02-23.PNG)
![](./assets/02-24.PNG)
![](./assets/02-25.PNG)
![](./assets/02-26.PNG)
![](./assets/02-27.PNG)



## Gouraud Shading    

![](./assets/02-28.PNG)

 - Barycentric weights allows the interior points of a triangle to be interpolated.     
 - In a traditional graphics pipeline, pixel colors are calculated at triangle vertices first, and then interpolated within. This is known as Gouraud shading.    
 - It is hardware accelerated.    
 - It is no longer popular.     
 
 
 

## Example 9: Tetrahedral Volume    


![](./assets/02-29.PNG)


## Example 9: Tetrahedral Volume



Note that the volume \\(\mathbf{V} =\frac{1}{3}h\mathit{A} =\frac{1}{6}\mathbf{x} _{30}\cdot (\mathbf{x}_{10}\times \mathbf{x}_{20})\\) **signed**.

![](./assets/02-30.PNG)



## Example 10: Barycentric Weights (cont.)


![](./assets/02-31.PNG)

## Example 11: Particle-triangle Intersection

![](./assets/02-32.PNG)


## Matrices  


## Matrix: Definition



A real matrix is a set of real elements arranged in rows and columns.


![](./assets/02-33.PNG)



## Matrix: Multiplication    

How to do matrix-vector and matrix-matrix multiplication? (Omitted)


![](./assets/02-34.PNG)


## Matrix: Orthogonality


An orthogonal matrix is a matrix made of orthogonal **unit** vectors. 


![](./assets/02-35.PNG)


## Matrix Transformation


A rotation can be represented by an orthogonal matrix.    

![](./assets/02-36.PNG)


A scaling can be represented by a diagonal matrix.  


![](./assets/02-37.PNG)


## Singular Value Decomposition   

A matrix can be decomposed into:     
\\(\mathbf{A=UDV^T}\\)such that \mathbf {D} is diagonal,and U and V are orthogonal.     
D 的对角线元素是**singular values**   
Any **linear deformation** can be decomposed into three steps: rotation, scaling and rotation:    


![](./assets/02-38.PNG)


## Eigenvalue Decomposition
A **symmetric** matrix can be decomposed into:     
\\(\mathbf{A=UDV^{-1}}\\)such that \mathbf {D} is diagonal,and U is orthogonal.     
D 的对角线元素是**eigenvalues**    

![](./assets/02-39.PNG)


We can apply eigenvalue decomposition to <u>asymmetric</u> matrices too, if we allow eigenvalues and eigenvectors to be **complex**. **Not considered here**.



## Symmetric Positive Definiteness (s.p.d.)   


![](./assets/02-40.PNG)

|  What does this even mean???   | 
|:----- |

![](./assets/02-41.PNG)


## Symmetric Positive Definiteness (s.p.d.)



 - **A** is s.p.d. if only if all of its eigenvalues are positive:     
 \\(\mathbf{A=UDU^T}  and d_o,d_1,\cdots > 0.\\)    

 - But eigenvalue decomposition is a stupid idea most of the time, since it takes lotsof time to compute.     
 - In practice, people often choose other ways to check  if **A** is sp.d. For example,    


![](./assets/02-42.PNG)


Finally, a s.p.d.matrix must be invertible:   
$$
\mathbf{A^{-1} =(U^T)^{-1}D^{-1}U^{-1} = UD^{-1}U^T}.
$$.


## Question   


Prove that if **A** is s.p.d., then \\(\mathbf{B} =\begin{bmatrix}
 \mathbf{A} &\mathbf{-A} \\
\mathbf{-A}  &\mathbf{A}
\end{bmatrix}\\)is symmetric semi-definite.     

For any\\( \mathbf{x} and \mathbf{y}\\), we know:

$$
\begin{bmatrix}
\mathbf{ x^T}&\mathbf{ y^T}
\end{bmatrix}\mathbf{B}\begin{bmatrix}
\mathbf{x} \\
\mathbf{y}
\end{bmatrix}=\begin{bmatrix}
\mathbf{ x^T}&\mathbf{ y^T}
\end{bmatrix}\begin{bmatrix}
 \mathbf{A} &\mathbf{-A} \\
\mathbf{-A}  &\mathbf{A}
\end{bmatrix}\begin{bmatrix}
\mathbf{x} \\
\mathbf{y}
\end{bmatrix}
$$

$$
\mathbf{=x^T(x-y)-y^TA(x-y)=(x-y)^TA(x-y)} 
$$



Since **A** is sp.d., we must have:    

$$
\begin{bmatrix}
 \mathbf{ x^T} & \mathbf{y^T} 
\end{bmatrix}\mathbf{B} \begin{bmatrix}
 \mathbf{x} \\
\mathbf{y} 
\end{bmatrix}\ge 0
$$





## Linear Solver    


Many numerical problems are ended up with solving a linear system:   


![](./assets/02-43.PNG)


It's expensive to compute \\(\mathbf{A^{-1}} \\), especially if \\(\mathbf{A} \\) is large and sparse. So we cannot simplydo:\\(\mathbf{x = A^{-1}b}\\).     

There are two popular linear solver approaches: direct and iterative.   




## Direct Linear Solver    


A direct solver is typically based LU factorization, or its variant: Cholesky, \\(LDL^T\\), etc…    

![](./assets/02-44.PNG)

![](./assets/02-45.PNG)
![](./assets/02-46.PNG)





## Direct Linear Solver    


 - When \\(\mathbf{A}\\)  is sparse, \\(\mathbf{L}\\) and \\(\mathbf{U}\\) are not so sparse. Their sparsity depends on the permutation.(See matlab)     
 - lt contains two steps: factorization and solving. lf we must solve many linear systems with the same \\(\mathbf{A}\\) , we can factorize it only once.        
 - Cannot be easily parallelized:Intel MKL PARDISO     






## Iterative Linear Solver    


An iterative solver has the form:   

![](./assets/02-47.PNG)


Why does it work?    

![](./assets/02-48.PNG)


So,

![](./assets/02-49.PNG)


\\(\rho\\):矩阵的spectral radius (the largest absolute value of the eigenvalues)


\\(\mathbf{M}\\) must be easier to solve:    
![](./assets/02-50.PNG)



The convergence can be accelerated: Chebyshev, Conjugate Gradient, … (Omitted here.)    

优点：
![](./assets/02-51.PNG)

缺点：

![](./assets/02-52.PNG)



## Tensor Calculus   


## Basic Concepts: 1st-Order Derivatives   


![](./assets/02-53.PNG)

![](./assets/02-54.PNG)

![](./assets/02-55.PNG)


## Basic Concepts: 1st-Order Derivatives    



![](./assets/02-56.PNG)




## Basic Concepts: 2nd-Order Derivatives    

If \\(f\mathbf{(x)\in R} \\),then:   

![](./assets/02-57.PNG)


秦勒展开
①\\(x\in R,f(x)\in R\\)     
$$
f(x)=f(x_0)+{f}' (x_0)(x-x_0)+\frac{1}{2} {f}'' (x_0)(x-x_0)^2+\cdots 
$$

②\\(x\in R^n,f(x)\in R\\)

$$
f(x)=f(x_0)+\rhd {f}' (x_0)\cdot (x-x_0)+\frac{1}{2}(x-x_0)^TH(x-x_0)+\cdots 
$$

当\\(H正定时,f(x)\\)满足一些特殊的性质





## Quiz:     


![](./assets/02-58.PNG) 


## Example: A Spring    


![](./assets/02-59.PNG)


Choi and Ko. 2002. Stable But Responive Cloth. TOG (SIGGRAPH)    



## Example: A Spring with Two Ends    


![](./assets/02-60.PNG)