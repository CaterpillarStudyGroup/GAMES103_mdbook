

P5  
# 相交检测

## 方法一：Spatial Partitioning    


Spatial partitioning divides the space by a grid and stores objects into grid cells.     

> &#x2705; 把空间划分成固定大小的格子，标记每个对象所占的格子。    

P6   

### 静止场景
To find pair candidates for collision test, we just have to check the grid cells.      

> &#x2705; 位于同一格子里的两个对象可能存在穿模。    

![](./assets/09-2.png)    

> &#x2705; 图中以三角形面片为例，但实际上对刚体和 bbox 同样适用。   

P7   
### 运动场景    

If we need to consider moving objects, we just expand the object region.    

![](./assets/09-3.png)    



P8   
### 数据存储    

  
Instead of allocating **memories** to cells, we can build an object-cell list and then sort them. This avoids memories wasted in empty cells.     

   
> &#x2705;要解决的问题：3D空间需要划分出大量的小格。有的格子可能包含很多object. 大多数格子可能没有object.    
> &#x2705;方法：3D数组转为list表示法。  
> &#x2705;缺点：内存访问不连续。   

![](./assets/09-5.png)    

P9   
#### Morton Code   

> &#x2705; Morton Code：一种对格子编号的顺序。   

One question is how to define the cell ID. Using the grid order is not optimal, since it cannot be easily extended and it is lack of locality. Morton code uses a Z-pattern instead.     

![](./assets/09-6.png)    

> &#x2705; 希望内存访问尽量连续。也就是下一次访问的内存地址在上次的附近    
> &#x2705; Grid Order：横向访问连续、纵向访问不连续、三维情况会更严重。   

![](./assets/09-7.png)    

P10   
## After-Class Reading   

GPU Gems 3    

Chapter 32. Broad-Phase Collision Detectionwith CUDA    



P14   
## 方法二：Bounding Volume Hierarchy    


**碰撞检测提供以信息：**    
1. 是否存在穿模     
2. 最快解除模的移动方向     
3. 解除穿模移动方向对应的矩离    

**碰撞检测层次：**    
1. 刚体 bbox 之间      
2. 刚体之间    
3. 三角形面片之间     

**其它：**     
1. 粗/精检测，是否能准确判断穿模情况，或是提供排除信息     
2. 是否支持多个对象之间碰撞检测     

输出：是否存在穿模(精)   
检测层次：1.2.3    
多对象检测：支持    


Bounding volume hierarchy is built on geometric/topological proximity of objects.     

> &#x2705;空间划分→物体划分   

P16  
## 构造Bounding Box   

<u>Axis-aligned bounding box (AABB)</u> is the most popular bounding volume. Besides that, there are also <u>spheres</u> and <u>oriented bounding box (OBB)</u>.     

Two AABBs intersect if and only if they intersect in every axis.     

## 构造BVH
![](./assets/09-8.png)    

P15   
## 外部物体与身体相交检测  

To find elements potentially in collision with an object, we just traverse the tree.    

![](./assets/09-9.png)    

P17    
## 自相交检测    

To process **self collisions** by BVH, we define two procedures.     

![](./assets/09-10-1.png)   


![](./assets/09-10.png)   


P18   
 
The performance depends on the effectiveness of 剪枝。    

|ID|Year|Name|Note|Tags|Link|
|---|---|---|---|---|---|
||2012|Energy-based Self-Collision Culling for Arbitrary Mesh Deformations|&#x2705; 对每个区域计算能量，根据形变能量的大小来判断有没有可能相交，此方法不适用于衣服，因为在衣服模拟中大形变很常见、不代表有相交。|


P19   
# Comparison between SH and BVH   


 - Spatial Hashing    
    - Easy to implement    
    - GPU friendly    
    - Needs to <u>recompute</u> after updating objects    

 - Bounding Volume Hierarchy    
    - More involved    
    - Not GPU friendly    
    - To update BVH, just update bounding volumes    
    
    
> &#x2705; CUDA 代码. NVIDIA 代码通常使用SH。GPU 喜欢简单粗爆的数据结构，BVH相对于GPU过于复杂。   



---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/