


P3  
## A Mass Spring System   



P4   
## An Ideal Spring    

An ideal spring satisfies Hooke’s law: the spring force tries to restore the rest length.    

![](./assets/05-1.PNG) 

![](./assets/05-2.PNG)    


\\(E(\mathbf{x})=\frac{1}{2}k (||\mathbf{x}_i −\mathbf{x}_j||−\mathbf{L} )^2\\)



\\(\mathbf{f} _i(\mathbf{x} )=−∇_i\mathbf{E} =−k(||\mathbf{x}_i −\mathbf{x}_j||−L)\frac{\mathbf{x}_i −\mathbf{x}_j}{||\mathbf{x}_i −\mathbf{x}_j ||}\\)



\\(\mathbf{f} _j(\mathbf{x})=−∇_jE=−k (||\mathbf{x}_j −\mathbf{x}_i ||−L)\frac {\mathbf{x}_j −\mathbf{x}_i}{||\mathbf{x}_j −\mathbf{x}_i||}\\)



P5  
## Multiple Springs   

When there are many springs, the energies and the forces can be simply summed up.     

![](./assets/05-3.PNG)    

$$
E= {\textstyle \sum_{e=0}^{3}}E_e= {\textstyle \sum_{e=0}^{3}} (\frac{1}{2} k(||\mathbf{x} _i −\mathbf{x}_e ||−L_e)^2)
$$



$$
f_i=−\nabla_iE = \textstyle \sum_{e=0}^{3}(−k(||\mathbf{x}_i−\mathbf{x}_e||−L_e)\frac{\mathbf{x}_i−\mathbf{x}_e}{||\mathbf{x}_i−\mathbf{x}_e||})
$$





P6  
## Structured Spring Networks   

![](./assets/05-4.PNG)    


P7  
## Unstructured Spring Networks   


We can also turn an unstructured triangle mesh into a spring network for simulation.    

![](./assets/05-5.PNG)  




P8   
## Triangle Mesh Representation   


The basic representation of a triangle mesh uses vertex and triangle lists. 

![](./assets/05-6.PNG)    

Vertex list: {\\(\mathbf{x} _0, \mathbf{x}_1, \mathbf{x}_2, \mathbf{x}_3, \mathbf{x}_4\\)}    (3D vectors)    

Triangle list: {1, 2, 3, 0, 1, 3, 0, 3, 4}    (index triples)    


| Each triangle has three edges. But there are repeated ones. |    
|----|   


P9   
## Topological Construction   

The key to topological construction is to sort triangle edge triples.    

![](./assets/05-7.PNG)    


Each triple contains: edge vertex index 0, edge vertex index 1 and triangle index (index 0<index). 

![](./assets/05-8.PNG)    


P11   
## Explicit Integration of A Mass-Spring System   

![](./assets/05-9.PNG)    



P12   
## Explicit Integration of A Mass-Spring System   

Explicit integration suffers from **numerical instability** caused by <u>overshooting</U>, when the stiffness \\(k\\) and/or the time step \\(∆t\\) is too large.     

A naive solution is to use a small \\(∆t\\) . But that slows down the simulation.    

![](./assets/05-10.PNG)    


P13  
## Implicit Integration    

Implicit integration is a better solution to numerical instability.  The idea is to integrate both **x** and **v** implicitly.   

![](./assets/05-11.PNG)    

消元得：    
![](./assets/05-12.PNG)    


Assuming that \\(\mathbf{f}\\) is *holonomic*, i.e., depending on \\(\mathbf{x}\\) only, our question is how to solve:    
$$
\mathbf{x} ^{[1]}=\mathbf{x}^{[0]}+∆t\mathbf{v} ^{[0]}+∆t^2\mathbf{M} ^{−1}\mathbf{f} (\mathbf{x}^{[1]})
$$






P14   

$$
\mathbf{‖x‖_M^2=x^TMx} 
$$

>\\(\mathbf{x} ^{[1]} =\\) argmin \\(F(\mathbf{x})\quad\\)  for   \\(\quad F(\mathbf{x}) = \frac{1}{2∆t^2}||\mathbf{x} −\mathbf{x} ^{[0]}−∆t\mathbf{v} ^{[0]}||_M^2+E(\mathbf{x} )\\)    


Note that this is applicable to every system, not just a mass-spring system.    



P15   
## Newton-Raphson Method   

The Newton-Raphson method, commonly known as Newton’s method, solves the optimization problem: \\(x^{[1]}\\) = argmin \\(F(x)\\).   

![](./assets/05-13.PNG)    

Given a current \\(x^{(k)}\\), we approximate our goal by: 

$$
0={F}' (x)≈{F}'(x^{(k)})+{F}'' (x^{(k)})(x−x^{(k)})
$$

![](./assets/05-14.PNG)    



P16    
Newton’s method finds an extremum, but it can be a minimum or maximum.    

![](./assets/05-15.PNG)    

 - At a minimum \\(x^∗, {F}'' (x^∗)>0\\).     
 - At a maximum \\(x^∗, {F}''(x^∗)<0\\). 
 - If \\({F}''(x)>0\\) is everywhere, \\(F(x)\\) has no maximum.  \\(=> F(x)\\) has only one minimum.     



P17  
## Newton-Raphson Method 解隐式积分优化问题    


Now we can apply Newton’s method to: \\(x^{[1]} \\)= argmin \\(F(x)\\).
Given a current \\(x^{(k)}\\), we approximate our goal by: 

$$
0=\nabla F( \mathbf{x}) ≈\nabla F (\mathbf{x} ^{(k)})+\frac{∂F ^2(\mathbf{x} ^{(k)})}{∂\mathbf{x} ^2} (\mathbf{x−x} ^{(k)}) 
$$

![](./assets/05-16.PNG)    



P18  
## Simulation by Newton’s Method    


Specifically to simulation, we have:   

$$
F (\mathbf{x} )=\frac{1}{2∆t^2}||\mathbf{x} −\mathbf{x} ^{[0]}−∆t\mathbf{v} ^{[0]}||_\mathbf{M} ^2+\mathbf{E} (\mathbf{x} )
$$

$$
∇F(\mathbf{x}^{(k)})=\frac{1}{∆t^2}\mathbf{M} (\mathbf{x} ^{(k)}−\mathbf{x} ^{[0]}−∆t\mathbf{v} ^{[0]})−\mathbf{f}(\mathbf{x}^{(k)})
$$

$$
\frac{∂^2F (\mathbf{x} ^{(k)})}{∂\mathbf{x} ^2} =\frac{1}{∆t^2} \mathbf{M} +\mathbf{H} (x^{(k)})
$$

> Initialize \\(\mathbf{x} ^{(0)}\\), often as \\(\mathbf{x} ^ {(0)}\\) or \\(\mathbf{x} ^{(0)} +∆t\mathbf{v} ^{(0)}\\)  
 For \\(k=0\dots K\\)   
 Solve \\((\frac{1}{∆t^2} \mathbf{M}+\mathbf{H}(\mathbf{x}^{(k)}))∆\mathbf{x}=− \frac{1}{∆t^2}\mathbf{M}(\mathbf{x}^{(k)}−\mathbf{x}^{[0]}−∆t\mathbf{v}^{[0]})+\mathbf{f}(\mathbf{x} ^{(k)})\\)    
 \\(\mathbf{x}^{(k+1)}←\mathbf{x}^{(k)}+∆\mathbf{x}\\)     
 If \\(||∆\mathbf{x} ||\\) is small	\\(\quad\\) then bre     
 \\(\mathbf{x} ^{[1]}←\mathbf{x} ^{(k+1)}\\)    
 \\(\mathbf{v} ^{[1]}←(\mathbf{x}^{[1]}−\mathbf{x} ^{[0]})/ ∆t\\)    



P19  
## SolveSpring Hessian

According to Lecture 2, Page 48,      

![](./assets/05-17.PNG)    


This is because for any \\(\mathbf{x} _ij, \mathbf{v} ≠0\\),    

$$
\mathbf{v}^\mathbf{T}\frac{{\mathbf{x}_{ij}\mathbf{x}_{ij}}^\mathbf{T}} {||\mathbf{x}_{ij}||^2}\mathbf{v}=||\frac{{\mathbf{x}_{ij}}^\mathbf{T}\mathbf{v}}{||\mathbf{x} _{ij}||}||^2 > 0
$$

$$
\mathbf{v}^\mathbf{T}\frac{\mathbf{x}_{ij}\mathbf{x}_{ij}{^\mathbf{T}}} {||\mathbf{x}_{ij}||^2}\mathbf{v} 
$$

$$
=||\frac{\mathbf{x}_{ij}{^\mathbf{T}}\mathbf{v}}{||\mathbf{x} _{ij}||}||^2 > 0
$$


$$
\mathbf{v} ^\mathbf{T} (\mathbf{I} -\frac{{\mathbf{x}_{ij}\mathbf{x}}^\mathbf{T}_{ij}} {||\mathbf{x}_{ij}||^2}) \mathbf{v} =\frac{||\mathbf{x} _{ij}||^2||\mathbf{v}||^2- ||{\mathbf{x}_{ij}}^\mathbf{T}\mathbf{v}||^2 }{||\mathbf{x} _{ij}||^2}\ge 0
$$




P20   
When a spring is stretched, \\(\mathbf{H} _e\\) is s.p.d.; but when it’s compressed, \\(\mathbf{H} _e\\) may not be s.p.d.     

As a result, \\(\mathbf{H} _x\\) may not be s.p.d. (Lecture 2, Page 36).    

\\(\mathbf{A}\\) may not be s.p.d. either.    

![](./assets/05-18.PNG)    

P22 

## Positive Definiteness of Hessian    

When a spring is compressed, the spring Hessian may not be positive definite. This means there can be multiple local minima (outcomes).    

![](./assets/05-19.PNG)    


Note: This issue occurs only in 2D and 3D. In 1D, \\((E)=\frac{1}{2} k(x−L)^2\\) and \\({E}''(x)=k>0\\).     



P23   
## Enforcement of Positive Definiteness   

 - Nevertheless, some linear solvers can fail to work if the matrix A in A∆x=b is not positive definite.    

 - One solution is to simply drop the ending term, when \\({\color{Orange} ||\mathbf{x} _{ij}||<\mathbf{L} _e}:\\)       


 ![](./assets/05-20.PNG)    


 - Other solutions exist. For example,     
    - Choi and Ko. 2002. Stable But Responive Cloth. TOG (SIGGRAPH)      



P24   
## The Jacobi Method    

We can use the Jacobi method to solve \\(\mathbf{A}\bigtriangleup \mathbf{x}  =\mathbf{b} \\).   

![](./assets/05-21.PNG)    



The vanilla Jacobi method (\\(α\\)=1) has a tight convergence requirement on **A**, i.e., being diagonal dominant.    

The use of \\(α\\) allows the method to converget even when **A** is positive definite only.    




P25   
## Linear Solvers – An Incomplete Summary    

|  Intel MKL PARDISO  |  
|-----|  

 - Direct Solvers (LU, LDLT, Cholesky, …)    
    - One shot, expensive but worthy if you need exact solutions.    
    - Little restriction on \\(\mathbf{A}\\)    
    - Mostly suitable on CPUs     

 - Iterative Solvers     
    - Expensive to solve exactly, but controllable    
    - Convergence restriction on \\(\mathbf{A}\\), typically positive definiteness    
    - Suitable on both CPUs and GPUs    
    - Easy to implement    
    - Accelerable: Chebyshev, Nesterov, <u>Conjugate Gradient</u>…    


P26   
## The Jacobi Method with Chebyshev Acceleration    

We can use the accelerated Jacobi method to solve \\(\mathbf{A}\bigtriangleup \mathbf{x}  =\mathbf{b} \\).    

> The Accelerated Jacobi Method    
> \\(∆\mathbf{x}  \longleftarrow \mathbf{0} \\)    
> last_\\(∆\mathbf{x}  \longleftarrow \mathbf{0}\\)   
> For \\(k=0\dots \mathbf{K}\\)   
\\(\mathbf{r}  \longleftarrow \mathbf{b} −\mathbf{A} ∆\mathbf{x}\\)    
If \\(||\mathbf{r} ||<\omega \quad\\)	break     
If  \\(k=0	\quad\quad \omega =1\\)   
Else \\(If  k=1 \omega =2/(2-\rho^2)\\)    
Else \\(\quad\quad\omega =4/(4-\rho ^2\omega )\\)      
old_\\(\bigtriangleup \mathbf{x} \longleftarrow \bigtriangleup \mathbf{x}\\)    
\\(∆\mathbf{x} ⟵∆\mathbf{x} +\mathbf{αD} ^{−1}\mathbf{r}\\)   
\\(∆\mathbf{x} \longleftarrow \omega ∆ \mathbf{x} +(1−\omega)\\)last_\\(∆\mathbf{x}\\）   
last_\\(∆\mathbf{x} \longleftarrow\\) old_\\(∆\mathbf{x}\\)    



\\(\rho  (\rho <1)\\) is the estimated spectral radius of the iterative matrix.    


P27   
## After-Class Reading   

Baraff and Witkin. 1998. Large Step in Cloth Simulation. SIGGRAPH.    

One of the first papers using implicit integration.     

The paper proposes to **use only one Newton iteration**, i.e., solving only one linear system. This practice is fast, but can fail to converge.    


P28   
## Bending and Locking Issues   

P29   
## The Bending Spring Issue    

A **bending** spring offers **little resistance** when cloth is nearly planar, since its length barely changes.     


![](./assets/05-22.PNG)    



P30   
## A Dihedral Angle Model

A dihedral angle model defines bending forces as a function of \\(\theta : \mathbf{f} _i=\mathbf{f} (\theta )\mathbf{u} _i\\).    

![](./assets/05-23.PNG)    

 - First, \\(\mathbf{u}_1\\) and \\(\mathbf{u}_2\\) should be in the normal directions \\(\mathbf{n}_1\\) and \\(\mathbf{n}_2\\).     

 - Second, bending doesn’t stretch the edge, so \\(\mathbf{u}_4\\)−\\(\mathbf{u}_3\\) should be orthogonal to the edge, i.e., in the span of \\(\mathbf{n}_1\\) and \\(\mathbf{n}_2\\).

 - Finally, \\(\mathbf{u}_1+\mathbf{u}_2+\mathbf{u}_3+\mathbf{u}_4=0\\), which means \\(\mathbf{u}_3\\) and \\(\mathbf{u}_4\\) are in the span of \\(\mathbf{n}_1\\) and \\(\mathbf{n}_2\\).    




P31    
Conclusion:

![](./assets/05-24.PNG)    



P32   

Planar case:    

> \\(\mathbf{f} _i=k\frac{||\mathbf{E}||^2}{||\mathbf{N}_1||+||\mathbf{N}_2||} \sin(\frac{π−\theta}{2})\mathbf{u} _i\\)    


Non-planar case:
$$
\mathbf{f} _i=k\frac{||\mathbf{E} ||^2}{||\mathbf{N} _1||+||\mathbf{N} _2||}(\sin(\frac{π−\theta}{2})-\sin(\frac{π−\theta_0}{2}))\mathbf{u}_i
$$



P33    
## After-Class Reading    

Bridson et al. 2003. *Simulation of Clothing with Folds and Wrinkles*. SCA.      

Explicit integration.     
Derivative is difficult to compute.    



P34    
## A Quadratic Bending Model     

A quadratic bending model has two assumptions: 1) planar case; 2) little stretching.      

![](./assets/05-25.PNG)    

$$
E(\mathbf{x} )=\frac{1}{2} \begin{bmatrix}
 \mathbf{x}_0 & \mathbf{x}_1 & \mathbf{x}_2 & \mathbf{x}_3
\end{bmatrix}\mathbf{Q} \begin{bmatrix}
\mathbf{x}_0 \\
\mathbf{x}_1 \\
 \mathbf{x}_2\\
\mathbf{x}_3
\end{bmatrix}
$$

$$
\mathbf{Q} =\frac{3}{\mathbf{A} _0+\mathbf{A} _1}\mathbf{qq^T}
$$

$$
\mathbf{q} = \begin{bmatrix}
 (\cot\theta _1+ \cot\theta _3)\mathbf{I} \\\\
 (\cot\theta _0+ \cot\theta _2)\mathbf{I} \\\\
 (-\cot\theta _0- \cot\theta _1)\mathbf{I} \\\\
(-\cot\theta _2- \cot\theta _3)\mathbf{I}
\end{bmatrix}
$$
\\(\mathbf{I}\\) is 3-by-3 identity.    

It’s not hard to see that: \\(\mathbf{E} (\mathbf{x} )=\frac{3||\mathbf{q} ^T\mathbf{x} ||^2}{2(A_0+A_1)}\\).  Also, \\(\mathbf{E} (\mathbf{x} )=0\\) when the triangles are flat.    


P35  
## Pros and Cons of The Quadratic Bending Model

 - Easy to implement:   



 - Compatible with implicit integration.    
 - No longer valid if cloth stretches much.    
 - Not suitable if the rest configuration is not planar.   
     - Cubic shell model.    
     - Projective dynamics model.    
 
 

P36   
## A Quadratic Bending
 
Bergou et al. 2006. *A Quadratic Bending Model for Inextensible Surfaces*. SCA.    



P37   
## The Locking Issue    

So far we talked about the mass-spring model and other bending models, **assuming cloth planar deformation and cloth bending deformation are independent**.     

Is it true? Think about a zero bending case. Can a simulator fold cloth freely?     




P38    

The fundamental reason is due to a short of degrees of freedoms (DoFs).    
For a <u>manifold</u> mesh, Euler’s formula says:#edges=3#vertices-3-#boundary_edges.     
So if edges are all hard constraints, the DoFs are only: 3+ #boundary_edges.    



P39   
## Shape Matching    


P40   
## Shape Matching   

The basic idea is to define a quadratic energy based on the rotated reference element. To do so, we split transformation into deformation + rotation.     


![](./assets/05-26.PNG)    




P41   
## Shape Matching

The basic idea is to define a quadratic energy based on the rotated reference element. To do so, we split transformation into deformation + rotation.


![](./assets/05-27.PNG)    


P42   
## Shape Matching   

We can then define the quadratic energy as:   

$$
\mathbf{E} (\mathbf{x} )=\frac{1}{2}||\mathbf{F−R} ||^2
$$

(\\(\mathbf{R}\\) is the rotation inside of \\(\mathbf{F}\\).  This energy tries to penalize the existence of \\(\mathbf{S}\\).     

Assuming that \\(\mathbf{R}\\) is constant, this \\(E(\mathbf{x})\\) becomes a quadratic function.  We can then derive the force and the Hessian.    

$$
E(\mathbf{x} ) =\frac{1}{2} ||\begin{bmatrix}
 \mathbf{x} _1-\mathbf{x} _0 &\mathbf{x} _2-\mathbf{x} _0
\end{bmatrix}\begin{bmatrix}
 \mathbf{r} _1-\mathbf{r} _0 &\mathbf{r} _2-\mathbf{r} _0
\end{bmatrix}^{−1}−\mathbf{R}||^2
$$


P43   
## A Summary For the Day    

 - A mass-spring system          
     - Planar springs against stretching/compression	- replaceable by co-rotational model
     - Bending springs				- replaceable by dihedral or quadratic bending
     - Regardless of the models, as long as we have \\(\mathbf{E} (\mathbf{x}\\), we can calculate force \\(\mathbf{f} (\mathbf{x} )=−∇ \mathbf{E} (\mathbf{x})\\) and Hessian \\(\mathbf{H} (\mathbf{x} )=∂E^2(\mathbf{x} )/∂\mathbf{x} ^2\\).  Forces and Hessians are stackable.    

 - Two integration approaches    
     - Explicit integration, just need force.  Instability
     - Implicit integration, as a nonlinear optimization problem      
     - One way is to use Newton’s method, which solves a linear system in every iteration:    

 $$
 (\frac{1}{∆t^2}\mathbf{M} +\mathbf{H} (\mathbf{x} ^{(k)}))∆\mathbf{x} =− \frac{1}{∆t^2} \mathbf{M} (\mathbf{x} ^{(k)}−\mathbf{x} ^{[0]}−∆t\mathbf{v} ^{[0]})+\mathbf{f} (\mathbf{x} ^{(k)})
 $$

 - There are a variety of linear solvers (beyond the scope of this class).    
 - Some simulators choose to solve only one Newton iteration, i.e., one linear system per time step.    
