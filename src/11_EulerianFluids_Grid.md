P3  
# A Grid Representation and Finite Differencing   

P4  
## A Regular Grid Representation    


![](./assets/11-01.png)   


> &#x2705; 把场定义在标准格子上的好处：(1)把物理量定义在格子的中心（2）计算导数或利用导数进行微分计算变得容易了。   
> &#x2705; 上节课grid用1D来表示2D，2D表示3D，不是真正的grid方法。   
> &#x1F50E; Central Differencing：L10.    
> &#x2705; 空间中任意位置的物理量由格子中心插值得出。   

P6   
### Finite Differencing on Grid   

The grid is very friendly with central differencing.   

### 一阶导数

![](./assets/11-2.png)   

| $$\frac{∂f_{i+0.5,j}}{∂x}≈\frac{f_{i+1,j}−f_{i,j}}{ℎ}$$  |
|---|

P7   
### 二阶导数

![](./assets/11-3.png)   



P8  
### Discretized Laplacian

We can then obtain the discretized Laplacian operator on grid.   

![](./assets/11-4.png)   

$$
\frac{∂^2f_{i,j}}{∂x^2}≈\frac{\frac{∂f_{i−0.5,j}}{∂x}−\frac{∂f_{i+0.5,j}}{∂x}}{ℎ}≈\frac{f_{i−1,j}+f_{i+1,j}−2f_{i,j}}{ℎ^2}
$$

$$
\frac{∂^2f_{i,j}}{∂y^2}≈\frac{\frac{∂f_{i,j+0.5}}{∂y}−\frac{∂f_{i,j−0.5}}{∂y}}{ℎ} ≈\frac{f_{i,j−1}+f_{i,j+1}−2f_{i,j}}{ℎ^2} 
$$

|  $$∆f_{i,j}=\frac{∂^2f_{i,j}}{∂x^2}+\frac{∂^2f_{i,j}}{∂y^2}≈\frac{f_{i−1,j}+f_{i+1,j}+f_{i,j−1}+f_{i,j+1−4}f_{i,j}}{ℎ^2} $$  |
|---| 


> &#x2705; 网格上的Laplace算子。   


P9   
### Boundary Conditions    

The boundary condition specifies \\(f_{i−1,j}\\) if it’s outside.

![](./assets/11-5.png)   

A **Dirichlet** boundary: \\(f_{i−1,j}=C\\)   

|$$ ∆f_{i,j}≈\frac{C+f_{i+1,j}+f_{i,j−1}+f_{i,j+1}−4f_{i,j}}{ℎ^2}$$|
|---|


A **Neumann** boundary: \\(f_{i−1,j}=f_{i,j}\\)  

|  $$∆f_ {i,j} ≈ \frac{f_ {i+1,j}+f_ {i,j−1}+f_ {i,j+1}−3f_{i,j}}{ℎ^2}$$ |
|----|


> &#x2705; 至少有一个边界使用Dirithlet．否则会全部收缩为0．   
> &#x2705; Neumann是约束相对关系，没有绝对数值，会有无穷多解。   


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/

