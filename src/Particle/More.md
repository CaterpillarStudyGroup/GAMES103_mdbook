# Ongoing Research    


 - How to make the simulation more efficient?   
 
 - How to make fluids incompressible?    
 
 - When simulating water, only use water particles, no air particles. So particles are sparse on the water-air boundary. How to avoid artifacts there?    
 
 - Using AI, not physics, to predict particle movement?    

## 非AI方法

|ID|Year|Name|Note|Tags|Link|
|---|---|---|---|---|---|
||2025|Implicit Position-Based Fluids|1. 构建隐式积分转优化问题的目标函数<br> 2. 使用GPU亲和的方式解优化问题中的线性系统 <br> 3. 近似H保证H的正定性 <br> 4. 使流体趋于平静的机制||[link](https://dl.acm.org/doi/epdf/10.1145/3757377.3764005)|

Lecture 2 [1:08:23]     
Lecture2[1:08:23]    

其它粒子仿真方法：    
Discrete element methed    
Moving Particle Semi-implicit     
Power Particle     
Peridynamic  

## AI方法

|ID|Year|Name|Note|Tags|Link|
|---|---|---|---|---|---|
||2024|Modeling the real world with high-density visual particle dynamics|

   

---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/