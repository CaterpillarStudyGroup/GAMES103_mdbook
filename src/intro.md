
P3    
## More About Prerequisites


 - The course is designed for    
    - Undergraduates in the 3rd or 4th year, or fresh graduates.     
 - Linear Algebra    
    - You Should know basic linear algebra concepts, such as vectors, matrices, linear systems, SVD...
 - Calculus     
    - You should know how to calculate basic derivatives and integrals; you should understand chain rules, gradients, etc.    
 - Programming Skills     
    - C, or C++, or C#, or Javascript    
 - Ready to <u>learn by yourself</u>    
 - The life will be much easier if you took    
    - Numerical methods (numerical linear algebra, numerical PDEs), finite element analysis, fluid dynamics...     


P10   
## Issues for Discussion Today      

 - What’s computer graphics?    
 - What’s computer graphics used for?    
 - What’s physics-based animation?    
 - What are the topics to be studied in this class?    


P11    
## Issues for Discussion Today     


 - What’s computer graphics?    
 - What’s computer graphics used for?    
 - What’s physics-based animation?    
 - What are the topics to be studied in this class?    
 
 
P14 
## Real-Time Graphics Pipeline     



![](./assets/01-1-1.PNG)   


P15  
The number of frames sent to display in a second is called the *frame rate*.    
For example, 24 FPS, 30 FPS, 60 FPS, …     



P17
## Animation Playback

![](./assets/01-1.PNG) 


P18
## Movie

![](./assets/01-2.PNG) 


P19
## Geometry: Three Representations     


![](./assets/01-3.PNG)   



 - A mesh contains:    
    - Vertices (nodes)    
    - Elements (triangles, polygons, tetrahedra…)    
 - Triangle mesh is the foundation of graphics.    
 - Problems:     
    - Meshing (Delaunay triangulation)    
    - Simplification/subdivision    
    - Mesh optimization (smoothing, flows…)     
    - Volume mesh    



P20
## Geometry: Three Representations    



![](./assets/01-4.PNG)    


P21
## Geometry: Three Representations    


![](./assets/01-5.PNG)    




 - A point cloud is simple.    
 - It can be raw data from surface scan.     
 - Problems:    
    - Mesh reconstruction from cloud    
    - (Re)-Sampling    
    - Neighborhood search    
    - …    


P22
## Geometry: Three Representations    


![](./assets/01-6.PNG) 



 - A grid partitions the space; a cell stores the physical quantities at that spot.    
 - Don’t confuse it with structured mesh.     
 - It’s often acquired from volumetric scan, e.g., CT. 
 - Problems:    
    - Memory cost (octree?)    
    - Volumetric rendering?    
    - …    



P23

## Rendering: Non-Photorealistic vs. Photorealistic

![](./assets/01-7.PNG)   



P27
## Character and Physics-Based Animation      

![](./assets/01-10.PNG) 



P36
## Computer Graphics for Augmented Reality (AR)


![](./assets/01-11.PNG)    


P37
## Issues for Discussion Today    



 - What’s computer graphics?    
 - What’s computer graphics used for?    
 - What’s physics-based animation?    
 - What are the topics to be studied in this class?    
 
 
P38 
 
## Animation Paradigm

![](./assets/01-12.PNG)   


 - The goal of animation is to **update the state in every time step**.    
 - The state can be:    
    - Position/orientation     
    - Velocity     
    - Appearance     
    - Density    
    - …     
 - The time step doesn’t have to match the frame rate.    
    - It’s common to animate multiple time steps then render one frame.    
    
    
P39
## Physics-Based Animation Topics    


![](./assets/01-13.PNG)    


P54
## Physics-Based Animation Topics    


![](./assets/01-14.PNG)   


P56
## Physics-Based Animation Topics

![](./assets/01-15.PNG)    


P58
## Issues for Discussion Today     



 - What’s computer graphics?    
 - What’s computer graphics used for?    
 - What’s physics-based animation?    
 - What are the topics to be studied in this class?    
 
 
 
P59
## Topics in This Class    

![](./assets/1-16.PNG)   

P60
## My Own Expertise    

![](./assets/01-17.PNG)   



