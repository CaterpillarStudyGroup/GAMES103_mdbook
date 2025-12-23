P41   
# 相交解除 Intersection Elimination   


P42   
## 对于有体积的物体

Eliminating cloth-volume and volume-volume intersections is straightforward: simply pushing vertices/edges in the volume out.     

![](./assets/09-32.png)    


P43   
## 对于没有体积的物体，Untangling Cloth问题    

The situation is complicated in cloth-cloth intersection, since we don’t have a clear definition of inside and outside.   

> &#x2705;P42适用于有体积的物体，但布没有封闭体积，两根线没有里面外面之分，因此相交时不知道哪一段是正确的。  

## 方法一

> &#x2705; 方法：对布分段，根据分段区域决定谁在上谁在下，以此为依据推动顶点。  

### 算法过程

Baraff et al. used flood-fill to segment cloth into regions and decided which region is in intersection. (**Cannot handle boundary well**.)    

![](./assets/09-33.png)    

Baraff et al. 2003. Untangling Cloth. TOG (SIGGRAPH)   


P44  
### 算法效果

![](./assets/09-34-1.png)    
 

> &#x2705;缺点：1. 难以处理边界；2. 对整个面进行评估，难以用于GPU.   



P45   
## 方法二    

Volino and Magnenat-Thalmann proposed to untangle cloth by reducing the
intersection contour.     
Their method can handle boundaries, but it doesn’t always work.    

![](./assets/09-35.png)    


> &#x2705; 两个面相交会产生一条曲线，目标是让曲线变短。优点：可以处理边界；缺点：基于局部优化、可用于 GPU。   
> &#x2705;可以处理边界情况，缩短边界也能解除相交。   


P46   
### After-Class Reading   


Volino and Magnenat-Thalmann et al. 2006. *Resolving
Surface Collisions through Intersection Contour
Minimization*. TOG (SIGGRAPH).   


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/