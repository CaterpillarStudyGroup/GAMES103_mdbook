P3
## Collision Detection   

P4  
## Collision Detection Pipeline    

![](./assets/09-1.png)    



P5    
## Spatial Partitioning    


Spatial partitioning divides the space by a grid and stores objects into grid cells.     



P6   

To find pair candidates for collision test, we just have to check the grid cells.      

![](./assets/09-2.png)    


P7   
## Spatial Partitioning    

If we need to consider moving objects, we just expand the object region.    

![](./assets/09-3.png)    



P8   
## Spatial Partitioning    

  
Instead of allocating **memories** to cells, we can build an object-cell list and then sort them. This avoids memories wasted in empty cells.     

![](./assets/09-4.png)    

![](./assets/09-5.png)    


> &#x2705; 用 hash 链表代替数组    



P9   
## Morton Code   

One question is how to define the cell ID. Using the grid order is not optimal, since it cannot be easily extended and it is lack of locality. Morton code uses a Z-pattern instead.     

![](./assets/09-6.png)    

![](./assets/09-7.png)    


> &#x2705; 希望内存访问尽量连续。也就是下一次访问的内存地址在上次的附近    
Cid Order：横向访问连续、纵向访问不连续、三维情况会更严重。   
Morton Code：一种对格子编号的顺序。   


P10   
## After-Class Reading   

GPU Gems 3    

Chapter 32. Broad-Phase Collision Detectionwith CUDA    



P14   
## Bounding Volume Hierarchy

Bounding volume hierarchy is built on geometric/topological proximity of objects.     

![](./assets/09-8.png)    



P15   
## Bounding Volume Hierarchy  

To find elements potentially in collision with an object, we just traverse the tree.    

![](./assets/09-9.png)    



P16  
## Bounding Volume Hierarchy   

<u>Axis-aligned bounding box (AABB)</u> is the most popular bounding volume. Besides that, there are also <u>spheres</u> and <u>oriented bounding box (OBB)</u>.     

Two AABBs intersect if and only if they intersect in every axis.     



P17    
## Bounding Volume Hierarchy    

To process **self collisions** by BVH, we define two procedures.     

|  Process_Node(A) <br> { <br> For every A’s child: B<br>Process_Node(B) <br> For every A’s children pair <B, C> <br> if B and C intersect <br> Process_Pair(B, C) <br> } |  
|:-----|  

$$\quad$$


| Process_Pair(B, C) <br> { <br> For every B’s child: B’<br>For every C’s child: C’ <br> if B’ and C’ intersect <br> Process_Pair(B’, C’)<br>}  |  
|:-----| 


![](./assets/09-10.png)   


P18   
## Bounding Volume Hierarchy   

The performance depends on the effectiveness of culling.    


| Process_Node(A) <br> { <br> For every A’s child: B<br>Process_Node(B) <br> For every A’s children pair <B, C><br> if B and C intersect ⟵ Zheng and James. 2012. *Energy-based Self-Collision Culling for Arbitrary Mesh Deformations*. TOG (SIGGRAPH) <br> Process_Pair(B, C)<br>}  |  
|:-----| 

$$\quad$$

| Process_Pair(B C)    <br>    { <br>    For every B’s child: B’ <br> For every C’s child: C’   <br>    if B’ and C’ intersect <br>  Process_Pair(B’, C’) <br>     } |  
|:-----|    

![](./assets/09-11.png)   


> &#x2705; 对每个区域计算能量，根据形变能量的大小来判断有没有可能相交，此方法不适用于衣服，因为在衣服模拟中大形变很常见、不代表有相交。   



P19   
## Comparison between SH and BVH   


 - Spatial Hashing    
    - Easy to implement    
    - GPU friendly    
    - Needs to <u>recompute</u> after updating objects    

 - Bounding Volume Hierarchy    
    - More involved    
    - Not GPU friendly    
    - To update BVH, just update bounding volumes    
    
    
> &#x2705; CUDA 代码. INVIDI 代码通常使用SH    
GPU 喜欢简单粗糙的数据结构，但树对于GPU过于复杂。   



P20   
## Collision Detection Pipeline    

![](./assets/09-12.png)   



> &#x2705; 图画得不对。 DCD 和CCD对输入的需求不同，但SH和 BVH 跟这两种输入不是 一一 对应的关系。   


P21   
## Discrete Collision Detection (DCD)    

DCD tests if any intersection exists in each state at discrete time instant: \\(\mathbf{x}^{[0]}\\), \\(\mathbf{x}^{[1]}\\), …

To a triangle mesh, the basic test is <u>edge-triangle intersection</u> test.     

![](./assets/09-13.png)   

![](./assets/09-14.png)   


> &#x2705; 则准确来说。DCD检测的不是碰撞，而是相交    
t 代表相交位置对应 \\(x_a\\) 和\\(x_b\\)的插值量     



P22   
## Tunneling   


DCD is simple and robust, but it suffers from the tunneling problem: objects penetrating through each other without being detected.     


![](./assets/09-15.png)   


> &#x2705; 相交和碰撞的区别：相交分析的是运动前后的就态、碰撞检测的是运动的过程未相交不一定无碰撞、P20页所谓的 D 还是 C,是以时间角度说的。   
tunneling problem：当物体运动特别快时，有可能的穿透另一物体而没有被检测到，常见于细薄物体、例如衣服     


P23   
## Continuous Collision Detection (CCD)    


CCD tests if any intersection exists between two states: \\(\mathbf{x} ^{[0]}\\) and \\(\mathbf{x} ^{[1]}\\).    

To a triangle mesh, there two basic tests: <u>vertex-triangle</u> and <u>edge-edge</u> tests.      

![](./assets/09-17.png)   

![](./assets/09-16.png)   


当四点共面时，构成的四面体体积为0、利用四面体的体积公式，可求出四点共面的时间 t.**这里的t是时间**    
假设运动是匀速的，\\(x_{30}(t)、 x_{10}(t)、x_{20}(t)\\)都是关于t的 线性函数，
一无三次方程有公式解，但用到\\(\sqrt[3]{\cdot}\\)，因此不建议使用,建议用牛顿法。  


P24   
## Continuous Collision Detection (CCD)   

CCD tests if any intersection exists between two states: \\(\mathbf{x} ^{[0]}\\) and \\(\mathbf{x} ^{[1]}\\).      

To a triangle mesh, there two basic tests: <u>vertex-triangle</u> and <u>edge-edge</u> tests.       

![](./assets/09-18.png)   

![](./assets/09-19.png)   


> &#x2705; 先求四点去面的 t 年  
解一元三次方程也不建议牛顿法，而是二分法，因为t的范围是[0,1]   


P25   
## Issues with CCD   


 - Floating-point errors, especially due to root finding of a cubic equation    
    - Buffering epsilons, but that causes **false positives**.     
    - Gaming GPUs often use single floating-point precision.   

 - Computational costs: more expensive than DCD.   
    - Some argue that broad-phase collision culling is the bottleneck.   

 - Difficulty in implementation.    
 

游戏 GPU 以单精度为主，因此要注意浮点误差问题。     


P26   
## After-Class Reading    


Bridson et al. 2002. *Robust Treatment of Collisions, Contact
and Friction for Cloth Animation. TOG (SIGGRAPH)*.    

Relative simple explicit integration of cloth dynamics    


P27   
## Interior Point Methods and Impact Zone Optimization    


P28   
## Two Continuous Collision Response Approaches    

Given the calculated next state \\(\mathbf{x} ^{[1]}\\), we want to update it into \\(\bar{\mathbf{x} } ^{[1]}\\), such that the path from \\(\mathbf{x} ^{[0]}\\) to \\(\bar{\mathbf{x} } ^{[1]}\\) is intersection-free.    

![](./assets/09-20.png)   


> &#x2705; 蓝色区域为安全区域     
内点法：从\\(x^{[0]}\\)出来，朝\\(x^{[1]}\\)走，并永远保证只在安全区域 走，直到不能走为止。    
Impact Zone 法，从\\(x^{[1]}\\)出发，反复优化结果（投影），直到回到安全区域为止。    


P29  
## Pros and Cons    


 - Slow.    
    - Far from solution.    
    - All of the vertices.    
    - Cautiously by small step sizes.    
 - Always succeed.   


![](./assets/09-21.png)   

 - Fast. 
    - Close to solution. 
    - Only vertices in collision (impact zones). 
    - Can take large step sizes. 
 - May not succeed.

![](./assets/09-22.png)   


内点：为保证每一步安全，步长不能太大，因此慢、哪怕\\(\dot{x}^{[1]}\\)最终没有到最佳位置，但能保证一定在安全区域，因此一定成功\\(x^{[0]}\\)和\\(x^{[1]}\\)可能比较远，也导致慢。   
Impact Zone：\\(x^{[1]}\\)通常离安全区域不太远，且优化时只针对 Impact Zone 优化，因此快。  



P30   
## Log-Barrier Interior Point Methods   

For simplicity, let’s consider the Log-barrier repulsion between two vertices.     

> $$E(\mathbf{x} )=−\rho \text{ log} ||\mathbf{x} _{ij}||$$    



> $$
\mathbf{f} _i(\mathbf{x} )=−∇_iE=ρ\frac{\mathbf{x} _ {ij}}{||\mathbf{x} _ {ij}||^2} \\\\
\mathbf{f} _j(\mathbf{x} )=−∇_jE=−ρ\frac{\mathbf{x} _ {ij}}{||\mathbf{x} _{ij}||^2}
$$

![](./assets/09-23.png)   


> &#x2705; 用 log 定义能量、前面某一节课讲过，   
不喜欢互斥力一直存在，因此做了一个截断（IPC）      



P31   
## Interior Point Methods – Implementation      

We can then formulate the problem as:   

$$
\bar{\mathbf{x} }^ {[1]}\longleftarrow \mathrm{argmin} _\mathbf{x} (\frac{1}{2} ||\mathbf{x} −\mathbf{x} ^{[1]}||^2−ρ\sum \mathrm{log} ||\mathbf{x} _{ij}||)
$$

Gradient Descent:    

>\\(\mathbf{x} ^{(0)}\longleftarrow \mathbf{x} ^{[0]}\\)   
For \\(k=0…K\\)    
$$\mathbf{x} ^{(k+1)}\longleftarrow \mathbf{x} ^{(k)}+α(\mathbf{x} ^{[1]}−\mathbf{x} ^{(k)}+ρ\sum \frac{\mathbf{x} _{ij}}{||\mathbf{x} _{ij}||^2})$$ 
\\(\bar{\mathbf{x} }^ {[1]}\longleftarrow \mathbf{x} ^{(k+1)}\\)


The step size \\({\color{Red} α}\\) must be adjusted to ensure that no collision happens on the way.  To find \\({\color{Red} α}\\), **we need collision tests**.    

![](./assets/09-24.png)   


> &#x2705; 绿色是来自\\(x^{[1]}\\)的引力，黄色是来自边界的斥力、关键是步长\\(\alpha \\)， 每走一小步都需要反复的碰撞检测。   



P32    
## Impact Zone Optimization    

The goal of impact zone optimization is to optimize \\(\mathbf{x}^{[1]}\\) until it becomes intersection-free. (This potentially suffers from the tunneling issue, but it’s uncommon.)     

$$
\bar{\mathbf{x} }^{[1]}\longleftarrow \mathrm{argmin} _\mathbf{x}  \frac{1}{2} ||\bar{\mathbf{x} }-\mathbf{x}^{[1]}||^2
$$  

$$
\text{such that}
\begin{cases}
 C(\mathbf{x} )=−(\mathbf{x} _3−b_0\mathbf{x} _0−b_1\mathbf{x} _1−b_2\mathbf{x} _1)\cdot \mathbf{N} ≤0 & \text{ For each detected vertex-triangle pair }  \\\\
 C(\mathbf{x} )=−(b_2\mathbf{x} _2+b_3\mathbf{x} _3−b_0\mathbf{x} _0−b_1\mathbf{x} _1)\cdot \mathbf{N}≤0 & \text{ For each detected edge-edge pair }
\end{cases}
$$

![](./assets/09-25.png)   


> &#x2705; 利用 constrain (不是能量）转化成优化问题具体没讲。  



P33   
## Geometric Impulse   

The goal of impact zone optimization is to optimize \\(\mathbf{x}^{[1]}\\) until it becomes intersection-free. (This potentially suffers from the tunneling issue, but it’s uncommon.)     

![](./assets/09-26.png)   

Every pair gives new positions to the involved vertices.  We can combine them together in a Jacobi, or Gauss-Seidel fashion, just like position-based dynamics.     




P34    
## After-Class Reading (Cont.)   


Bridson et al. 2002. *Robust Treatment of Collisions, Contact
and Friction for Cloth Animation. TOG (SIGGRAPH)*.     

Relative simple explicit integration of cloth dynamics     



P35   
## Augmented Lagrangian     

$$
\bar{\mathbf{x} }^{[1]}\longleftarrow \text{argmin} _\mathbf{x}  \frac{1}{2} ||{\mathbf{x} }-\mathbf{x}^{[1]}||^2
$$  

$$
\text{such that}
\begin{cases}
 C(\mathbf{x} )=−(\mathbf{x} _3−b_0\mathbf{x} _0−b_1\mathbf{x} _1−b_2\mathbf{x} _1)\cdot \mathbf{N} ≤0 & \text{ For each detected vertex-triangle pair }  \\\\
 C(\mathbf{x} )=−(b_2\mathbf{x} _2+b_3\mathbf{x} _3−b_0\mathbf{x} _0−b_1\mathbf{x} _1)\cdot \mathbf{N}≤0 & \text{ For each detected edge-edge pair }
\end{cases}
$$

![](./assets/09-27.png)  



P36   
## Augmented Lagrangian    


We can then convert it into an unconstrained form:   

$$\bar{\mathbf{x} } {[1]}\longleftarrow \text{argmin}_{x,λ}(\frac{1}{2} ||\mathbf{x} −\mathbf{x} ^{[1]}||^2+\frac{ρ}{2} ||\text{max}(\tilde{C}  (\mathbf{x} ))||^2−\frac{1}{2ρ}||\mathbf{λ} ||^2)
$$

$$
\tilde{C}  (\mathbf{x})= \text{max}(\mathbf{C} (\mathbf{x} )+\mathbf{λ} /ρ)
$$


Augmented Lagrangian:    

> \\(\mathbf{x} ^{(0)} \longleftarrow \mathbf{x} ^{[0]}\\)    
\\(\mathbf{λ \longleftarrow 0} \\)    
For \\(k=0…K\\)    
$$\mathbf{x} ^{(k+1)} \longleftarrow \mathbf{x} ^{(k)}−α∇(\frac{1}{2} ||\mathbf{x} −\mathbf{x} ^{[1]}||^2+\frac{ρ}{2} ||\text{max}(\tilde{C} (\mathbf{x} ))||^2−\frac{1}{2ρ}||\mathbf{λ} ||^2)$$  
\\(λ\longleftarrow ρ\tilde{C} (\mathbf{x} )\\)   
\\(\bar{\mathbf{x} } ^{[1]}\longleftarrow \mathbf{x} ^{(k+1)}\\)


Tang et al. 2018. I-Cloth: *Incremental Collision Handling for GPU-Based Interactive Cloth Simulation*. TOG. (SIGGRAPH Asia)    


P37   
## About Impact Zone Optimization   

 - Fast per iteration    
    - Only have to deal with vertices in collision.    

 - Convergence sensitive to \\(||\mathbf{x} ^{[0]}−\mathbf{x} ^{[1]}||^2\\), or the time step \\(∆t\\)      
    - Can take many iterations to, or never achieve *intersection-free*.   
    - Easy solution is to reduce \\(∆t\\), but that increases total costs.    


![](./assets/09-28.png)    



P38    
## Rigid Impact Zones    


The rigid impact zone method simply freezes vertices in collision from **moving in their pre-collision state**. It’s simple and safe, but has noticeable artifacts.     

![](./assets/09-29.png)    


P39   
## A Practical System   

![](./assets/09-30.png)    



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



P44  
## Untangling Cloth    

![](./assets/09-34-1.png)    

Baraff et al. 2003. Untangling Cloth. TOG (SIGGRAPH)    


P45   
## Untangling Cloth    

Volino and Magnenat-Thalmann proposed to untangle cloth by reducing the
intersection contour.     
Their method can handle boundaries, but it doesn’t always work.    

![](./assets/09-35.png)    


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
