

P2  
## Last week…  


In practice, we update the same state variable \\(\mathbf{s} =\\){\\(\mathbf{v,x,\omega ,q}\\)} over time.     


![](./assets/04-1.PNG)     



P3   
## What is a torque?   


A torque is the rotational equivalent of a force. It describes the rotational <u>tendency</u> caused by a force.    


![](./assets/04-2.PNG)     


\\(\mathbf{τ} _i\\) is perpendicular to both vectors: \\(\mathbf{Rr} _i\\) and \\(\mathbf{f} _i\\).    

\\(\mathbf{τ} _i\\) is porportional to ||\\(\mathbf{Rr} _i\\)|| and ||\\(\mathbf{f} _i\\)||.    


\\(\mathbf{τ} _i\\) is porportional to \\(\sin \theta\\).     
(\\(\theta\\)  is the angle between two vectors.)

|\\(\mathbf{τ} _i\longleftarrow (\mathbf{Rr} _i)\times \mathbf{f} _i\\)|   
|----|




P6   

## What is an inertia tensor?    



Similar to mass, an inertia tensor describes the resistance to rotational tendency caused by torque. But different from mass, it’s not a constant.    



![](./assets/04-3.PNG)     



Which side receives greater resistance?     



P7   
## What is an inertia tensor?   


It’s a matrix! The mass inverse is the resistance (just like mass).    



![](./assets/04-4.PNG)     

\\(\mathbf{I} _{\mathbf{ref} }=\sum m_i(\mathbf{r} _i^\mathbf{T} \mathbf{r} _i\mathbf{1} −\mathbf{r} _i\mathbf{r} _i^\mathbf{T} )\\)

\\(\mathbf{1}\\)  is the 3-by-3 identity.



![](./assets/04-5.PNG)     

What about the current inertia?      




\\(\mathbf{I} =\sum m_i(\mathbf{r} _i^\mathbf{T}\mathbf{R}  ^\mathbf{T}\mathbf{Rr}  _i\mathbf{1} −\mathbf{Rr} _i\mathbf{r} _i^\mathbf{T} \mathbf{R^T} )\\)   

\\(\quad=\sum m_i(\mathbf{Rr} _i^\mathbf{T}\mathbf{r}  _i\mathbf{1R}  ^\mathbf{T} −\mathbf{Rr} _i\mathbf{r} _i^\mathbf{T} \mathbf{R^T} )\\) 

\\(\quad=\sum m_i\mathbf{R}(\mathbf{r}_i^\mathbf{T}\mathbf{r}_i\mathbf{1}−\mathbf{r}_i\mathbf{r}_i^\mathbf{T} ) \mathbf{R^T}\\)   

\\(\quad=\mathbf{RI_{ref}R^T}\\)    



   

P10  
## Particle Collision Detection and Response    


P11  
## Signed Distance Function   


A <u>signed</u> distance function \\(\phi (\mathbf{x} )\\) defines the distance from \\(\mathbf{x}\\) to a surface with a signThe sign indicates on which side \\(\mathbf{x}\\) is located.     


![](./assets/04-6.PNG)     



P12   
## Signed Distance Function Examples    


![](./assets/04-07.PNG)     



P13   
## Intersection of Signed Distance Functions    

![](./assets/04-8.PNG)     

> If \\(\phi _0(\mathbf{x} )<0\\) and \\(\phi_1(\mathbf{x} )<0\\) and \\(\phi_2(\mathbf{x} )<0\\)      
then inside    
\\(\phi (\mathbf{x} )\\)=max \\(⁡(\phi_0(\mathbf{x}),\phi_1(\mathbf{x}),\phi_2(\mathbf{x}))\\)     
Else outside    
\\(\phi (\mathbf{x})=?\\)   


P14  
## Union of Signed Distance Functions   


![](./assets/04-9.PNG)     

Intuitively, we can consider collision detection with the union of two objects as **collision detection with two separate objects**.     


P15   
## Quadratic Penalty Method    



A penalty method applies a penalty force in the next update. When the penalty potential is quadratic, the force is linear.     

![](./assets/04-11.PNG)     

![](./assets/04-10.PNG)     


P16   
## Quadratic Penalty Method with a Buffer   


A buffer helps lessen the penetration issue. But it cannot strictly prevent penetration, no matter how large \\(k\\) is.      

![](./assets/04-12.PNG)     
![](./assets/04-13.PNG)     



P17   
## Log-Barrier Penalty Method     


A log-barrier penalty potential ensures that the force can be large enough. But it assumes \\(\phi (\mathbf{x} ) < 0\\) will never happen!!! To achieve that, it needs to adjust \\(\Delta t\\).     

![](./assets/04-14.PNG)     

![](./assets/04-15.PNG)     



P18  
## A Short Summary of Penalty Methods    



 - The use of step size adjustment is a must.     
    - To avoid overshooting.    
    - To avoid penetration in log-barrier methods.    

 - Log-barrier method can be limited within a buffer as well.    
    - Li et al. 2020. *Incremental Potential Contact: Intersection- and Inversion-free Large Deformation Dynamics*. TOG.    
    - Wu et al. 2020. *A Safe and Fast Repulsion Method for GPU-based Cloth Self Collisions*. TOG.   

 - Frictional contacts are difficult to handle.    
 
 
 
P19   
## Impulse Method    



An impulse method assumes that collision changes the position and the velocity all of sudden.      

![](./assets/04-16.PNG)    

![](./assets/04-17.PNG)    


P20    
Changing the position is not enough, we must change the velocity as well.      


![](./assets/04-18.PNG)    


P21   
## Rigid Body Collision Detection and Response   


P23   
## Rigid Body Collision Detection   


![](./assets/04-19.PNG)    


When the body is made of many vertices, we can detect its collision by testing each vertex:     

$$
\mathbf{x}_i\longleftarrow  \mathbf{x} +\mathbf{Rr} _i
$$

No a perfect solution, but acceptable (will come back to this weeks later…)     



P24   
## Rigid Body Collision Response by Impulse


![](./assets/04-20.PNG)    



Vertex *i*:    

![](./assets/04-21.PNG)    

Problem: **we cannot directly modif**y \\(\mathbf{x}_i\\) or \\(\mathbf{v}_i\\) **isince they not state variables**. They areindirectly determined.     


Solution: we will find a way to modify \\(\mathbf{v}\\) and \\(\mathbf{\omega}\\).     

   


P25   
思考过程：   
What happens to \\(\mathbf{V}_i\\) when an impulse \\(\mathbf{j}\\) is appliedat vertex \\(i\\)?      

![](./assets/04-22.PNG)    



P27    

$$
\mathbf{v_i^{new}} = \mathbf{v} _i+\frac{1}{M}\mathbf{j} −(\mathbf{Rr} _i)×(\mathbf{I} ^{−1}(\mathbf{Rr} _\mathbf{i}\times \mathbf{j} ))
$$

$$
\mathbf{v_i^{new}} = \mathbf{v} _i+\frac{1}{M} \mathbf{j} −(\mathbf{Rr} _i)^∗\mathbf{I} ^{−1} (\mathbf{Rr} _i)^∗\mathbf{j} 
$$


> 
>$$
>\mathbf{v_i^{new}}-\mathbf{v}_i=\mathbf{Kj}
>$$
>$$
>\mathbf{K} \longleftarrow \frac{1}{M} \mathbf{1} −(\mathbf{Rr} _i)^{∗}\mathbf{I} ^{−1}(\mathbf{Rr} _i)^{∗}
>$$
> 

P26   
## Cross Product as a Matrix Product    

We can convert the cross product \\(\mathbf{r}x\\) into a matrix product \\(\mathbf{r}^*\\).    

![](./assets/04-23.PNG)    



P28  
## Rigid Body Collision Response by Impulse    

![](./assets/04-24.PNG)    


P29  
## Some Implementation Details    



 - If there are many vertices in collision, we use their position average.     

 - We can decrease the restitution \\(\mathbf{\mu_N} \\) to reduce oscillation.     

 - We don't update the position here. Why?      
    - Because the problem is nonlinear.     
    - We will come back to this later when we talk about constraints.      






P30   
## Rigid Body Collision Response by Impulse    


![](./assets/04-25.PNG)    

Relative velocity at joints     

$$
\begin{cases}
 \mathbf{v} _0 ^{\mathbf{new} }− \mathbf{v} _0=\mathbf{K} _{a00 }\mathbf{j} _0+\mathbf{K} _{a01 }\mathbf{j} _1 −(−\mathbf{K} _{b00 }\mathbf{j} _0 +\mathbf{K} _{b02}\mathbf{j} _2 )\\\\
 \mathbf{v} _1 ^{\mathbf{new} }− \mathbf{v} _1=\mathbf{K} _{a10 }\mathbf{j} _0+\mathbf{K} _{a11 }\mathbf{j} _1 −(−\mathbf{K} _{c11 }\mathbf{j} _0 +\mathbf{K} _{c13 }\mathbf{j} _3 )\\\\
 \mathbf{v} _2 ^{\mathbf{new} }− \mathbf{v} _2=\mathbf{K} _{b20 }\mathbf{j} _0+\mathbf{K} _{b22 }\mathbf{j} _2\\\\
\mathbf{v} _3 ^{\mathbf{new} }− \mathbf{v} _3=\mathbf{K} _{c31 }\mathbf{j} _1+\mathbf{K} _{c33 }\mathbf{j} _3
\end{cases}
$$

$$
\Downarrow
$$


$$
\begin{bmatrix}
 \mathbf{K} _{a00 }+\mathbf{K} _{b00 } & \mathbf{K} _{a01 } & -\mathbf{K} _{b02 } & \Box \\\\
 \mathbf{K} _{a10 } & \mathbf{K} _{a11 }+\mathbf{K} _{c11 } & \Box  & -\mathbf{K} _{c13 }\\\\
 -\mathbf{K} _{b20 } & \Box  & \mathbf{K} _{b22} & \Box \\\\
 \Box  & -\mathbf{K} _{c31 } & \Box  & \mathbf{K} _{c33 } 
\end{bmatrix}\begin{bmatrix}
 \mathbf{j} _{0 }\\\\
 \mathbf{j} _{1}\\\\
 \mathbf{j} _{2}\\\\
\mathbf{j} _{3}
\end{bmatrix}=\begin{bmatrix}
 \bigtriangleup \mathbf{v} _{0}\\\\
 \bigtriangleup \mathbf{v} _{1}\\\\
 \bigtriangleup \mathbf{v} _{2}\\\\
\bigtriangleup \mathbf{v} _{3}
\end{bmatrix}
$$


\\(\mathbf{K} _{a01}\mathbf{j} _1\\) stands for the velocity change of bunny \\(a\\) at joint 0, caused by impulse \\(\mathbf{j}_1\\).






P31  
## After-Class Reading (Before Collision)    



<https://graphics.pixar.com/pbm2001>     
Rigid Body Dynamics


P32    
## Shape Matching    


P33  
## Basic Idea    


We allow each vertex to have its own velocity, so it can move by itself.     

![](./assets/04-26.PNG)    



First, move vertices **independently** by its velocity, with collision and friction being handled.     

Second, enforce the **rigidity** constraint to become a rigid body again.      



P34  
## Mathematical Formulation    

Now \\(\mathbf{c}\\) and \\(\mathbf{R}\\) are unknowns we want to find out from:

![](./assets/04-27.PNG)    



P35  
## Mathematical Formulation   


![](./assets/04-28.PNG)    


P36   
## Remember that…   


Singular value decomposition says any matrix can be decomposed into: rotation,scaling and rotation: \\(\mathbf{A = UDV} ^T\\).    

![](./assets/04-29.PNG)    

We can rotate the object back before the final rotation: \\(\mathbf{A}  = (\mathbf{UV} ^T)(\mathbf{VDV} ^T)\\).    

![](./assets/04-30.PNG)    


P37   
We can rotate the object back before the final rotation: \\(\mathbf{A}  = (\mathbf{UV} ^T)(\mathbf{VDV} ^T)\\).    

![](./assets/04-31.PNG)    






P38  
## Polar Decomposition     

![](./assets/04-32.PNG)    

$$
\mathbf{A=RS} 
$$

$$
\mathbf{A} ^T\mathbf{A}  = \mathbf{S} ^T\mathbf{S}  = \mathbf{S} ^2
$$

分解结果:unique   



## Shape Matching    



| Independent Update <br> For every vertex <br>\\(\mathbf{f} _i\longleftarrow   \mathbf{Force}  (\mathbf{x} _i, \mathbf{v} _i)\\)<br>\\(\mathbf{v} _i\longleftarrow \mathbf{v} _i + \bigtriangleup tm_i^{-1}\mathbf{f} _i\\)<br>\\(\mathbf{y} _i \longleftarrow  \mathbf{x}_i + \bigtriangleup t\mathbf{v} _i\\)|   
|----|


\\(<br>\\)  

|Rigidify the vertices<br>\\(\mathbf{c} =\frac{1}{N}\sum_i\mathbf{y} _i\\)<br>\\(\mathbf{A} =(∑ _i(\mathbf{y} _i−\mathbf{c} ) \mathbf{r} _i^\mathbf{T} )(∑_i\mathbf{r} _i \mathbf{r} _i^\mathbf{T} )^{−1}\\)<br>\\(\mathbf{R} =\mathrm{Polar} (\mathbf{A} )\\)|   
|----|

\\(<br>\\) 

|Update \\(\mathbf{v}_i\\) and \\(\mathbf{x}_i\\)<br>For every vertex<br>\\(\mathbf{v}_i\longleftarrow (\mathbf{c} +\mathbf{Rr}_i−\mathbf{x}_i)/∆t\\)<br>\\(\mathbf{x}_i\longleftarrow \mathbf{c} +\mathbf{Rr}_i\\)|
|---|   




Physical quantities are attached to each vertex, not to the entire body.   



P40  
## Shape Matching    


 - Easy to implement and compatible with other nodal systems, i.e., cloth, soft bodies and even particle fluids.    

 - Difficult to strictly enforce friction and other goals.     
    - The rigidification process will destroy them.    

 - More suitable when the friction accuracy is unimportant, i.e., buttons on clothes.    
 
 
 P41   
## After-Class Reading    

Muller et al. 2005.    
*Meshless Deformations Based on Shape Matching*. TOG (SIGGRAPH).     