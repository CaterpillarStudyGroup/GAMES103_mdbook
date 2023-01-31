
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
 - Ready to learn by yourself    
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


![](\assets\01-1.png)    



The number of frames sent to display in a second is called the *frame rate*.    
For example, 24 FPS, 30 FPS, 60 FPS, …     




## Animation Playback

![](\assets\01-2.png)   

## Movie

![](\assets\01-3.png)   



## Geometry: Three Representations     


![](\assets\01-4.png)   



 - A mesh contains:    
    - Vertices (nodes)    
    - Elements (triangles, polygons, tetrahedra…)    
 - Triangle mesh is the foundation of graphics.    
 - Problems:     
    - Meshing (Delaunay triangulation)    
    - Simplification/subdivision    
    - Mesh optimization (smoothing, flows…)     
    - Volume mesh    




## Geometry: Three Representations    



![](\assets\01-5.png)   



## Geometry: Three Representations    


![](\assets\01-6.png)   




 - A point cloud is simple.    
 - It can be raw data from surface scan.     
 - Problems:    
    - Mesh reconstruction from cloud    
    - (Re)-Sampling    
    - Neighborhood search    
    - …    



## Geometry: Three Representations    


![](\assets\01-7.png)   



 - A grid partitions the space; a cell stores the physical quantities at that spot.    
 - Don’t confuse it with structured mesh.     
 - It’s often acquired from volumetric scan, e.g., CT. 
 - Problems:    
    - Memory cost (octree?)    
    - Volumetric rendering?    
    - …    





## Rendering: Non-Photorealistic vs. Photorealistic

![](\assets\01-8.png)   
![](\assets\01-9.png)   
![](\assets\01-10.png)   


## Character Animation Physics-Based Animation


![](\assets\01-11.png)   



## Issues for Discussion Today    

![](\assets\01-12.png)   


 - What’s computer graphics?    
 - What’s computer graphics used for?    
 - What’s physics-based animation?    
 - What are the topics to be studied in this class?    
 
 
 
 
## Animation Paradigm

![](\assets\01-12.png)   


 - The goal of animation is to **update the state in every time step**.    
 - The state can be:    
    - Position/orientation     
    - Velocity     
    - Appearance     
    - Density    
    - …     
 - The time step doesn’t have to match the frame rate.    
    - It’s common to animate multiple time steps then render one frame.    
    
    

## Physics-Based Animation Topics    


![](\assets\01-13.png)   



## Physics-Based Animation Topics    


![](\assets\01-14.png)   



## Physics-Based Animation Topics

![](\assets\01-15.png)   



## Issues for Discussion Today     



 - What’s computer graphics?    
 - What’s computer graphics used for?    
 - What’s physics-based animation?    
 - What are the topics to be studied in this class?    
 
 
 

## Topics in This Class    

![](\assets\01-16.png)   


## My Own Expertise    

![](\assets\01-17.png)   



