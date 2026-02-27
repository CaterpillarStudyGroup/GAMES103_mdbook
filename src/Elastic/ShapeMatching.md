P24  
## Shape Matching

Shape matching is also projective dynamics, if we view rotation as projection:    

|
![](../assets/06-15.png)    

|**The 2D Space**|**The 3D Space**|    
|---|---|    
|![](../assets/06-013.png)|![](../assets/06-014.png)|



Assuming that \\(\mathbf{{\color{Orange} R} }\\) is constant,     
$$
\begin{matrix}
 \mathbf{f} _0=−\nabla_0E(\mathbf{x} )\\\\
\mathbf{f} _1=−\nabla_1E(\mathbf{x} ) \\\\
\mathbf{f} _2=−\nabla_2E(\mathbf{x} )\\\\
\mathbf{H} =\frac{∂E^2(\mathbf{x} )}{∂x^2} \quad \text{is  a constant !}   
\end{matrix}
$$


P25   
## Simulation by Projective Dynamics   

 - According to implicit integration and Newton’s method, a projective dynamics simulator looks as follows, with matrix \\(\mathbf{A} =\frac{1}{∆t^2}\mathbf{M+}\mathbf{H} \\) being constant.    

 - We can use a direct solver with **only one factorization of A**.
 
## Pipeline    

Initialize  \\(\mathbf{x} ^{(0)}\\), often as\\( \mathbf{x} ^{[0]} \\)or \\(\mathbf{x} ^{[0]} +∆t\mathbf{v} ^{[0]} \\)    

For \\(k=0\dots K\\)     
\\(\quad\\) Recalculate projection     

\\(\quad\\) Solve \\((\frac{1}{∆t^2}\mathbf{M} +\mathbf{H} )∆\mathbf{x} =−\frac{1}{∆t^2}\mathbf{M} (\mathbf{x} ^{(k)}−\mathbf{x} ^{[0]}−∆t\mathbf{v} ^{[0]})+\mathbf{f} (\mathbf{x} ^{(k)})\\)    

\\(\quad\\) \\(\mathbf{x} ^{(k+1)}\longleftarrow \mathbf{x} ^{(k)}+∆\mathbf{x} \\)      

\\(\quad\\) If \\(||∆\mathbf{x}||\\) is small	\\(\quad\\) then break     

\\(\mathbf{x} ^{[1]}\longleftarrow \mathbf{x} ^{(k+1)}\\)    

\\(\mathbf{v} ^{[1]}\longleftarrow (\mathbf{x} ^{[1]}-\mathbf{x} ^{[0]})/∆t\\)


P27  
## Pros and Cons of Projective Dynamics 

### Pros

 - By building constraints into energy, the simulation now has a theoretical <u>solution</u> with **physical** meaning.    
 - **Fast on CPUs** with a direct solver. No more factorization!    


> &#x2705; Fast on CPU,因为它只作一次\\(\mathbf{LU}\\)分解。   
 - Fast convergence in the first few iterations.    

### Cons

 - **Slow on GPUs**. (GPUs don’t support direct solver wells.)    
> &#x2705; Slow on GPU，因为\\(\mathbf{LU}\\)分解不适用于 \\(\mathbf{GPU}\\)   
 - Slow convergence over time, as it fails to consider Hessian caused by projection.     
    - Still suffering from high stiffness    
 - Cannot easily handle **constraint changes**.   
    - Contacts    
    - Remeshing due to fracture, etc.   

> &#x2705; constraint changes: 网格关系改变导至弹簧结构改变，原来的\\(\mathbf{H}\\)将不再适用。    
       


> &#x2705; 课后答疑：   
能量优化的方法很少用于刚体，主要是有限元、弹性体、衣服模拟。   
