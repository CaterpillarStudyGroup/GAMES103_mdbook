P36   
## A Summary For the Day   

 - The **Eulerian grid** presentation is very friendly with finite **differencing**. This makes calculus a lot easier.    
 - For **velocity** fields, we can use **staggered grid**.    

 - For low-speed, incompressible, viscous flow, we need to solve the Navier-Stokes equations.    
 - To solve the equations, we can do this in step-by-step (method of characteristics). 
 
 - To simulate air and water, we need to advect some physical quantities.   
    - Smoke (density); water (volume-of-fluid, or signed distance  function)    
    - **Volume loss** issue in water (how to fix it?)    
    - If you need to create a mesh from grid for rendering, you need something like <u>marching cube</u>.   


> &#x2705; 用有限元方法也能模拟水，但难以模拟流动性。流动需要对四面体重新构造，成本很高。    



---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/