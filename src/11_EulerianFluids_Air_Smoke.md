P31   
# Air and Smoke   


> &#x2705; 前面讲的是怎么更新速度；后面讲怎么利用速度做出效果。 



P32   
## Air Simulation   

 - Air simulation is done in two steps.   
 - In Step 1, we update the flow (the velocity field) \\(\mathbf{u}\\).   
 - In Step 2, we use semi-Lagrangian (page 22) advect all of the other physical quantities, i.e., density, temperature…   
 - Typically we use Dirichlet boundaries for an open space (or Neumann boundaries for a container.)   
 - We can use it to simulate underwater as well.   

 
P33   
## Water Simulation

> &#x2705; 要渲染的不是水，而是水与空气的接触面。但通常只模拟水不模拟空气。  

 - Two representations   
    - Volume-of-fluid (as the name suggests…)   
    - A signed distance function defined over the grid.   
> &#x2705; 表示1：例如一个格子存储水的体积的百分化。用于早期，无法描述水的界面，因此不精准。   

 - How to advect(更新)?    
    - Semi-Lagrangian (volume loss)   
    - Level set method (volume loss)   
    - Needs corrections.   

> &#x2705; advect 2：专用于更新 SDF 的方法。       
> &#x2705; 水变少是常见问题，两种advect都存在。    




P35   
## After-Class Reading   


Osher and Fedkiw.    
Level Set Methods and Dynamic Implicit Surfaces.    

> &#x2705; 介绍流体模拟的很好的书。   

---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/