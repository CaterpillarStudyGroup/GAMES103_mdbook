
P1   
## GAMES103: Intro to Physics-Based Animation

Eulerian Fluids

Huamin Wang

Dec 2021


P2  
## Topics for the Day   


 - A Grid Representation and Finite Differencing  

 - Incompressible, Viscous Navier Stokes’ equations  

 - Air and liquid  
 
 
 
P3  
## A Grid Representation and Finite Differencing   


P4  
## A Regular Grid Representation    


![](./assets/11-01.png)   



P5  
## Central Differencing   



P6   
## Finite Differencing on Grid   


The grid is very friendly with central differencing.   

![](./assets/11-2.png)   

| $$\frac{∂f_{i+0.5,j}}{∂x}≈\frac{f_{i+1,j}−f_{i,j}}{ℎ}$$  |
|---|




P7   
## Finite Differencing on Grid

The grid is very friendly with central differencing.    

![](./assets/11-3.png)   


P8  
## Discretized Laplacian

We can then obtain the discretized Laplacian operator on grid.   

![](./assets/11-4.png)   

$$
\frac{∂^2f_{i,j}}{∂x^2}≈\frac{\frac{∂f_{i−0.5,j}}{∂x}−\frac{∂f_{i+0.5,j}}{∂x}}{ℎ}≈\frac{f_{i−1,j}+f_{i+1,j}−2f_{i,j}}{ℎ^2}
$$

$$
\frac{∂^2f_{i,j}}{∂y^2}≈\frac{\frac{∂f_{i,j+0.5}}{∂y}−\frac{∂f_i,j−0.5}{∂y}}{ℎ} ≈\frac{f_{i,j−1}+f_{i,j+1}−2f_{i,j}}{ℎ^2} 
$$

|  $$∆f_{i,j}=\frac{∂^2f_{i,j}}{∂x^2}+\frac{∂^2f_{i,j}}{∂y^2}≈\frac{f_{i−1,j}+f_{i+1,j}+f_{i,j−1}+f_{i,j+1−4}f_{i,j}}{ℎ^2} $$  |
|---| 


P9   
## Boundary Conditions    

The boundary condition specifies f_i−1,j if it’s outside.

![](./assets/11-5.png)   

A Dirichlet boundary: \\(f_{i−1,j}=C\\)   

|$$ ∆f_{i,j}≈\frac{C+f_{i+1,j}+f_{i,j−1}+f_{i,j+1}−4f_{i,j}}{ℎ^2}$$|
|---|


A Neumann boundary: \\(f_{i−1,j}=f_{i,j}\\)  

|  $$∆f_{i,j}≈\frac{f_{i+1,j}+f_{i,j−1}+f_{i,j+1}−3f_{i,j}}{ℎ^2} |
|----|



P12   
## Diffusion

The process of applying Laplacian smoothing is called **diffusion**.     



P13  
## Problem with Central Differencing   

Central differencing gives the derivative in the middle.    

![](./assets/11-6.png)   

 - The cell doesn’t exist at (i+0.5, j).   

 - To get \\(\frac{∂f_{i,j}{∂x} \\), we need \\(f_{i−1,j}\\) and f_i+1,j.  But this is weird, because \\(f_{i,j}\\) is unused.    





P14  
## Solution: Staggered Grid   

We define some physical quantities on faces, specifically **velocities**.    

![](./assets/11-7.png)   



 - The x-part of the velocity is defined on vertical faces.   

- The y-part of the velocity is defined on horizonal faces.   

- **Intuitively**, they represent the flow speed between two cells. For example, we write the volume changing speed at cell (i,j) as:   


|  $$u_{i+1,j}+v_{i,j+1}−u_{i,j}−v_{i,j}$$  |
|---|  



P15  
## Divergence-Free Condition

No volume change is equal to say the fluid is incompressible. This can be formally written as a divergence-free velocity field.   

![](./assets/11-8.png)   


P16   
## Bilinear Interpolation   


P18   
## <u>Incompressible, Viscous</u>  Navier-Stokes Equations 


P19  
## Equation Fomulation   

![](./assets/11-9.png)   

 - Method of Characteristics: solving a long partial differential equation (PDE) in steps
 - Step 1: Update \\(\mathbf{u}\\) by solving \\(∂\mathbf{u}∕∂t=\mathbf{g}\\)   
 - Step 2: Update \\(\mathbf{u}\\) by solving \\(∂\mathbf{u}∕∂t=−(\mathbf{u}∙∇)\mathbf{u}\\)  
 - Step 3: Update \\(\mathbf{u}\\) by solving \\(∂\mathbf{u}∕∂t=υ∆\mathbf{u}\\)  
 - Step 4: Update \\(\mathbf{u}\\) by solving \\(∂\mathbf{u}∕∂t=−∇p\\)   
 


P20   
## Step 1: External Acceleration


The Update of \\(\mathbf{u}\\) by \\(∂\mathbf{u}∕∂t=\mathbf{g}\\) is straightforward, just add acceleration to \\(u\\) and \\(v\\).    

![](./assets/11-10.png)   



P21  
## Step 2: Advection   

Next we need to update \\(\mathbf{u}\\) by solving \\(∂\mathbf{u}∕∂t=−(\mathbf{u}∙∇)\mathbf{u}\\).   

![](./assets/11-11.png)   

| $$(\mathbf{u} \cdot ∇)\mathbf{u} =u\cdot \frac{∂u}{∂x} +v\cdot \frac{∂v}{∂\mathbf{y}} $$ |
|---|  

Solving this in an Eulerian way can be a source of instability.   

To solve this problem, we come to realize that advection means to carry physical quantities by velocity.   




P22  
## Solution: Semi-Lagrangian Method   


The solution is to trace a virtual particle backward over time.   

![](./assets/11-12.png)   

 - Define \\(\mathbf{x}_0←(i−0.5, j)\\)   
 - Compute \\(\mathbf{u}(\\(\mathbf{x}_0)\\)   
 - \\(\mathbf{x}_1←\mathbf{x}_0−∆t \mathbf{u}(\mathbf{x}_0)\\)   
 - Compute \\(\mathbf{u}(\mathbf{x}_1)\\)
 - \\(u_i,j^{new}←u(\mathbf{x}_1)\\)   


Note that if the velocities are staggered, we need to do staggered bilinear interpolation.   




fP23  
## Solution: Semi-Lagrangian Method

The solution is to trace a virtual particle backward over time.    

![](./assets/11-13.png)   

 - Define \\(\mathbf{x}_0←(i, j−0.5)\\)    
 - Compute \\(\mathbf{u}(\mathbf{x}_0)\\)   
 - \\(\mathbf{x}_1←\mathbf{x}_0−∆t \mathbf{u}(\mathbf{x}_0)\\)   
 - Compute \\(\mathbf{u(\mathbf{x}_1)\\)   
 - v_{i,j}^{new}←v(\mathbf{x}_1)\\)   


P24   
## Solution: Semi-Lagrangian Method   

We could also subdivided the time step for better tracing.   

![](./assets/11-14.png)   


P25   
## Step 3: Diffusion  


![](./assets/11-15.png)   

$$
u_{i,j}^{new}←u_{i,j}+υ∆t\frac{u_{i−1,j}+u_{i+1,j}+u_{i,j−1}+u_{i,j+1}−4u_{i,j}}{ℎ^2} 
$$

$$
v_{i,j}^{new}←v_{i,j}+υ∆t\frac{v_{i−1,j}+v_{i+1,j}+v_{i,j−1}+v_{i,j+1}−4v_{i,j}}{ℎ^2}
$$

If \\(υ∆t\\) is large, the above formulae can be **unstable**.      



P26   
## Step 3: Diffusion

We could also use even smaller sub-steps…   



P27  
## Step 4: Pressure Projection    

Finally, we need to update u by solving ∂u∕∂t=−∇p. 

![](./assets/11-16.png)   

Staggering makes this very straightforward:

$$
u_{i,j}^{new}←u_{i,j}−\frac{∆t}{ℎ}(p_{i,j}−p_{i−1,j})
$$

$$
v_{i,j}^{new}←v_{i,j}−\frac{∆t}{ℎ}(p_{i,j}−p_{i,j−1})
$$

But what is \\(\mathbf{p}\\)?



P28   
## Step 3: Pressure Projection

The pressure is caused by incompressibility.     

![](./assets/11-17.png)   

In other words, after this update by pressure, we should achieve:   

|$$∇\cdot \mathbf{u}^{new}=0$$|  
|-------|

which means

> $$u_{i+,j}^{new}+v_{i,j+1}^{new}−u_{i,j}^{new}−v_{i,j}^{new}=0$$

$$
\Downarrow
$$

>$$ 
\begin{matrix}
u_{i+1,j}−(\frac{p_{i+1,j}−p_{i,j})}{ℎ}+v_{i,j+1}−\frac{(p_{i,j+1}−p_{i,j})}{ℎ} \\\\
−u_{i,j}−\frac{(p_{i,j}−p_{i−1,j})}{ℎ} −v_{i,j}−\frac{(p_{i,j}−p_{i,j−1})}{ℎ}=0
\end{matrix}$$



P29  
## Step 3: Pressure Projection   

The pressure is caused by incompressibility. Eventually, we get a Poisson equation:  

![](./assets/11-18.png)   

Eventually, we get a Poisson equation:   

$$
4p_{i,j}−p_{i−1,j}−p_{i+1,j}−p_{i,j−1}−p_{i,j+1}= \\\\
\\\\
ℎ(−u_{i+1,j}−v_{i,j+1}+u_{i,j}+v_{i,j})
$$


with boundary conditions:   

$$ \text{Dirichlet boundary (open) } p_{i−1,j}=P \\\\
\text{Neumann boundary (close) } p_{i−1,j}=p_{i,j}$$

Once we solve \\(\mathbf{p}\\), we update u and done.   




P30    
## After-Class Reading    


Jos Stam. 1999. *Stable Fluids. TOG (SIGGRAPH)*.   



P31   
## Air and Smoke   


P32   
## Air Simulation   

 - Air simulation is done in two steps.   
 - In Step 1, we update the flow (the velocity field) \\(\mathbf{u}\\).   
 - In Step 2, we use semi-Lagrangian (page 22) advect all of the other physical quantities, i.e., density, temperature…   
 - Typically we use Dirichlet boundaries for an open space (or Neumann boundaries for a container.)   
 - We can use it to simulate underwater as well.   

![](./assets/11-19.png)   



P33   
## Water Simulation


 - Two representations   
    - Volume-of-fluid (as the name suggests…)   
    - A signed distance function defined over the grid.    
 - How to advect?    
    - Semi-Lagrangian (volume loss)   
    - Level set method (volume loss)   
    - Needs corrections.   

![](./assets/11-20.png)   

But what if there is an air-water boundary???    


P34   
## Water Simulation   

 - Two representations   
    - Volume-of-fluid (as the name suggests…)   
    - A signed distance function defined over the grid.   

 - How to advect?   
    - Semi-Lagrangian (volume loss)   
    - Level set method (volume loss)   
    - Needs corrections.   


![](./assets/11-21.png)   

But what if there is an air-water boundary???   


P35   
## After-Class Reading   


Osher and Fedkiw.    
Level Set Methods and Dynamic Implicit Surfaces.    



P36   
## A Summary For the Day   

 - The **Eulerian** grid presentation is very friendly with finite **differencing**. This makes calculus a lot easier.    
 - For **velocity** fields, we can use **staggered grid**.    

 - For low-speed, incompressible, viscous flow, we need to solve the Navier-Stokes equations.    
 - To solve the equations, we can do this in step-by-step (method of characteristics). 
 
 - To simulate air and water, we need to advect some physical quantities.   
    - Smoke (density); water (volume-of-fluid, or signed distance  function)    
    - **Volume loss** issue in water (how to fix it?)    
    - If you need to create a mesh from grid for rendering, you need something like <u>marching cube</u>.   