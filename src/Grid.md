## Physics-Based Animation Topics    
P56


![](./assets/01-15.png)    


> &#x2705; 

> 流体：烟通常使用粒子法或网格法。水波可以看作是整体，因此能用 mesh，用 mesh的好处是可以做到实时，Grid 的好处是更真实。Splashes(水花)的问题是多变，因此不能实时，通常使用粒子和网格。   
> Hybrid 方法：MPM = Particle + Grid,兼容二者优点，常用于模拟雪或粘滞物体   
Coupling: 场景中同时有不同类别的物体，怎样模拟它们的交互。   
> &#x2705; SPA 与弹性体模拟结合，可用于模拟物体破碎， 粒子法与网格法相结合，称为 MPM. 用于模拟雪、沙子。 

P59
## Topics in This Class    

![](./assets/1-16.png)   


> &#x2705;   
> Fracture 有大量的 remesh。游戏引擎中的 Fracture 通常通过预计算而不是模拟得到。     
Rigid 还是Soft,看有没有形变。   
Mesh 定义在物体上， Grid 定义在场景上   
水波 Mesh 也会讲，图上漏掉了。 