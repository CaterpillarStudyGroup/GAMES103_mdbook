
P40   
## Untangling Cloth    


P41   
## Intersection Elimination   


 - Let’s consider how to eliminate existing intersections, but without using any collision history.   
 
 - Such a method is useful when there are already intersections in simulation, due to:    
    - Past collision handling failures
    - Intense user interaction
 - In this case, we don’t require the simulation is to always <u>intersection-free</u>.     
 
 ![](./assets/09-31.png)    


> &#x2753; 相交解除跟碰撞处理有什么区别？   



P42   
## Intersection Elimination

Eliminating cloth-volume and volume-volume intersections is straightforward: simply pushing vertices/edges in the volume out.     

![](./assets/09-32.png)    




P43   
## Untangling Cloth    

The situation is complicated in cloth-cloth intersection, since we don’t have a clear definition of inside and outside.      

Baraff et al. used flood-fill to segment cloth into regions and decided which region is in intersection. (**Cannot handle boundary well**.)    

![](./assets/09-33.png)    

Baraff et al. 2003. Untangling Cloth. TOG (SIGGRAPH)   


> &#x2705; 两根线没有里面外面之分，因此相交时不知道哪一段是正确的。此方法缺点：1. 无法处理边界；2. 难以在 GPU 上实 现；  

> &#x2705;P42适用于有体积的物体，但布没有封闭体积，没有里外。   
方法：对布分段，根据分段区域决定谁在上谁在下，以此为依据推动顶点。   



P44  
## Untangling Cloth    

![](./assets/09-34-1.png)    

Baraff et al. 2003. Untangling Cloth. TOG (SIGGRAPH)    

> &#x2705;缺点：1. 难以处理边界；2. 对整个面进行评估，难以用于GPU.   



P45   
## Untangling Cloth    

Volino and Magnenat-Thalmann proposed to untangle cloth by reducing the
intersection contour.     
Their method can handle boundaries, but it doesn’t always work.    

![](./assets/09-35.png)    


> &#x2705; 两个面相交会产生一条曲线，目标是让曲线变短。优点：可以处理边界；缺点：基于局部优化、可用于 GPU。   

> &#x2705;可以处理边界情况，缩短边界也能解除相交。   


P46   
## After-Class Reading   


Volino and Magnenat-Thalmann et al. 2006. *Resolving
Surface Collisions through Intersection Contour
Minimization*. TOG (SIGGRAPH).   


P47   
## A Summary For the Day   

 - Collision handling involves two steps: *collision detection* and *collision response*.    
 
 - Collision detection contains two phases: *broad-phase culling* and *narrow-phase test*.    
 
 - There are two types of collision detection tests: *discrete* and *continuous*.    
 
 - Similarly, there are discrete and continuous collision responses.   
 
 - For continuous collision responses, we must update the state to become collisionfree state. There are two approaches: *interior point method* and *impact zone optimization*. **Rigid impact zone is also a method, but it’s problematic**.    

 - For discrete collision responses, we allow intersections to stay and hope to remove them in long turn. **Cloth-cloth intersections are difficult to handle**.    


> &#x2705; 考虑摩擦，通常把摩擦做为后处理，但这样结果不精确。如果同时处理摩擦和碰撞、会很复杂。   

> &#x2705;Impulse方法的碰撞检测通常用SDF．但很多形变体无法使用SDF.    
Impulse响应方式是离散响应方式，无法处理穿透问题。   
碰撞开源代码：bullet. physics X   


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/