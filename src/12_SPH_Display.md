P28   
## Fluid Display   


• Need to reconstruct the water surface from particles!    


![](./assets/12-15.png)   


> &#x2705; 点云转成三角面片用于渲染也是一个比较复杂的问题。    
> &#x2705;（1）平滑方法：bias kemal（见GAMES 102）    
> &#x2705;（2）把球转为SDF，SDF转为Mesh    



P29   
## Ongoing Research    


 - How to make the simulation more efficient?   
 
 - How to make fluids incompressible?    
 
 - When simulating water, only use water particles, no air particles. So particles are sparse on the water-air boundary. How to avoid artifacts there?    
 
 - Using AI, not physics, to predict particle movement?    





---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/