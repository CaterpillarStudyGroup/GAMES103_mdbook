
P2   
## What is rigid body dynamics?     

P3  
## Rigid Bodies    

Our living environment is stuffed with rigid objects.



P6  
## Rigid Body Simulation   



The goal of simulation is to update the state variable \\(\mathbf{s} ^{[k]}\\) over time.     


![](./assets/03-1.PNG)     



P7   
## Rigid Body Motion  


If a rigid body cannot deform, its motion consists of two parts: translation and rotation.   


![](./assets/03-2.PNG)     


P9
## Translational Motion    


P10
## Translational Motion   


![](./assets/03-3.PNG)     


For translational motion, the state variablecontains the position \\(\mathbf{x}\\) and the velocity \\(\mathbf{v}\\).     

 

$$
\begin{cases}
 \mathbf{v} (t^{[1]})=\mathbf{v} (t^{[0]})+\mathbf{M} ^{−1}\int_{t^{[0]}}^{t^{[1]}} \mathbf{f} (\mathbf{x} (t), \mathbf{v} (t), t)dt\\\\
\mathbf{x} (t^{[1]})=\mathbf{x} (t^{[0]})+\int_{t^{[0]}}^{t^{[1]}} \mathbf{v} (t)dt
\end{cases}
$$

| integration |  
|----|  



P11   
## Integration Methods Explained    

By definition, the integral \\(\mathbf{x} (t) = \int \mathbf{v}  (t) dt\\) is the area. Many methods estimate the area as a box.   

![](./assets/03-4.PNG) 

![](./assets/03-5.PNG) 


P12   
## Integration Methods Explained    

![](./assets/03-6.PNG) 

![](./assets/03-7.PNG) 


P13  
## Integration Methods Explained   

![](./assets/03-8.PNG) 

![](./assets/03-9.PNG) 



P14
## Integration Methods Explained   

By definition, the integral \\(\mathbf{x} (t)=∫\mathbf{v} (t) dt\\) is the area.  Many methods estimate the area as a box.    


|Explicit Euler (1st-order accurate) sets the height at \\(t^{[0]}\\).<br>  \\(\int_{t^{[0]}}^{t^{[1]}} \mathbf{v} (t)dt≈∆t  \mathbf{v} (t^{[0]})\\)|   
|---|      
  

\\(\quad\\)

|  Implicit Euler (1st-order accurate) sets the height at \\(t^{[0]}\\).<br>  \\(\int_{t^{[0]}}^{t^{[1]}} \mathbf{v} (t)dt≈∆t  \mathbf{v} (t^{[1]})\\) |  
|----|  
      
\\(\quad\\)

|  Mid-point (2nd-order accurate) sets the height at \\(t^{[0]}\\).<br>  \\(\int_{t^{[0]}}^{t^{[1]}} \mathbf{v} (t)dt≈∆t  \mathbf{v} (t^{[0.5]})\\) |     
|----|


![](./assets/03-10.PNG)    



P15   
## Translational Motion    


$$
\begin{cases}
 \mathbf{v} (t^{[1]})=\mathbf{v} (t^{[0]})+\mathbf{M} ^{−1}\int_{t^{[0]}}^{t^{[1]}} \mathbf{f} (\mathbf{x} (t), \mathbf{v} (t), t)dt\\\\
\mathbf{x} (t^{[1]})=\mathbf{x} (t^{[0]})+\int_{t^{[0]}}^{t^{[1]}} \mathbf{v} (t)dt
\end{cases}
$$



P16 
## Leapfrog Integration    


![](./assets/03-11.PNG)    


In some literature, such a approach is called *semi-implicit*.  

It has a funnier name: the *leapfrog method*.

![](./assets/03-12.PNG)    



P17  
## Types of Forces  


![](./assets/03-13.PNG)    


P18  
## igid Body Simulation (Translation Only)    


![](./assets/03-14.PNG)    

![](./assets/03-15.PNG)    

The mass \\(M\\) and the time step \\(\Delta t\\) are user-specified variables.     



P19  
## Rotational Motion


P20   
## Rotation Represented by Matrix     


 - The matrix representation is widely used for rotational motion.    
 - It’s friendly for applying rotation to each vertex (by <u>matrix-vector multiplication</u>).    

 - But it is not suitable for dynamics:   
    - It has too much redundancy: 9 elements but only 3 DoFs.    
    - It is non-intuitive.     
    - Defining its time derivative (*rotational velocity*) is also difficult.   
    


P21  
## Rotation Represented by Euler Angles    


 - The Euler Angles representation is also popular, often in design and control.    
 - It is intuitive. It uses three axial rotations to represent one general rotation. Each axial rotation uses an angle.     
 - In Unity, the order is rotation-by-Z, rotation-by-X, then rotation-by-Y.     

 - But it is not suitable for dynamics either:    
    - It can lose DoFs in certain statuses: gimbal lock.    
    - Defining its time derivative (rotational velocity) is difficult.    
    



P22  
## Gimbal Lock   


The alignment of two or more axes results in a loss of rotational DoFs.     

![](./assets/03-16.PNG)    



P23  
## Rotation Represented by Quaternion    

![](./assets/03-17.PNG)    

In the complex system, two numbers represent a 2D point.   

>  What about a “complex” system for 3D point? **Quaternion**! Four numbers represent a 3D point (with multiplication and division).    



P24   
## Quaternion Arithematic    


Let \\(\mathbf{q}  = \begin{bmatrix}
\mathbf{s}   &\mathbf{v} 
\end{bmatrix} \\) be a quaternion made of two parts: a scalar part \\(s\\) and a 3D vector part \\(\mathbf{v}\\), accounting for \\(\mathbf{ijk}\\).

\\(\quad\\)    

\\(a\mathbf{q} =\begin{bmatrix}
 as  &a\mathbf{v} 
\end{bmatrix}\quad\\) Scalar-quaternion Multiplication    

\\(\mathbf{q} _1±\mathbf{q} _2 =\begin{bmatrix}
 \mathbf{s}_1±\mathbf{s}_2  & \mathbf{v} _1 ± \mathbf{v} _2
\end{bmatrix}\quad\quad\\) Addition/Subtraction    


\\(\mathbf{q} _1×\mathbf{q} _2= \begin{bmatrix}
 \mathbf{s} _1\mathbf{s} _2−\mathbf{v} _1\cdot \mathbf{v} _2 & \mathbf{s} _1\mathbf{v} _2+\mathbf{s} _2\mathbf{v} _1+\mathbf{v} _1×\mathbf{v} _2
\end{bmatrix}\quad\quad\\) Multiplication   

\\(||\mathbf{q} ||=\sqrt{\mathbf{s^2+v\cdot v} } \quad\quad\\)Magnitude    

\\(\quad\\)    






P25   
## Rotation Represented by Quaternion    



 - To represent a rotation around \\(\mathbf{v}\\) by angle \\(0\\), we set the quaternion as:    

   ![](./assets/03-19.PNG)    

 - lt's very intuitive. lt's the built-in representation in Unity.     
 - Convertible to the matrix:   


$$
R=\begin{bmatrix}
s^2+x^2-y^2-z^2  & 2(xy-sz) & 2(xz+sy)\\\\
 2(xy+sz) & s^2-x^2+y^2-z^2 & 2(yz-sx) \\\\
 2(xz-sy) & 2(yz+sx) & s^2-x^2-y^2+z^2  
\end{bmatrix}
$$



P27   
## Rotational Motion    


![](./assets/03-20.PNG)    

Now we choose quaternion \\(\mathbf{q}\\) to represent theorientation, i.e., the rotation from the *reference* to the *current*.    

We use a 3D vector \\(\mathbf{\omega}\\) to denote angularvelocity.    

 
> The direction of \\(\mathbf{\omega}\\) is the axis.     
The magnitude of \\(\mathbf{\omega}\\) is the speed.    

![](./assets/03-21.PNG)     



P28   
## Torque and Inertia

![](./assets/03-22.PNG)     


P29   
## Translational and Rotational Motion   


|    |Translational (linear)|Rotational (Angular)|
|---|---|---|
|Updafe|![](./assets/03-23.PNG)   |![](./assets/03-24.PNG)   |
|states| Velocity \\(\mathbf{v}\\) <br> Position \\(\mathbf{x}\\)|Angular velocity \\(\mathbf{ω} \\)<br>   Quaternion \\(\mathbf{q}\\) |
| Physical Quantities |Mass \\(\mathbf{M}\\) <br> Force \\(\mathbf{f}\\) | Inertia \\(\mathbf{I} \\) <br> Torque \\(\mathbf{τ} \\) |







P30 
## Rigid Body Simulation    


![](./assets/03-27.PNG)     

平移：   
![](./assets/03-25.PNG)     

旋转：   
![](./assets/03-26-1.PNG)     



P32   
## Some More lssues
 - Gravity doesn't cause any torque! lf your simulator does not contain any other force, there is no need to update \\(\mathbf{\omega}\\).    


P33
## After-Class Reading (Before Collision)



<https://graphics.pixar.com/pbm2001>     
Rigid Bdy Dyunis    



