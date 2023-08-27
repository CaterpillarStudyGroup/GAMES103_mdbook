P18   
# Nonlinear Optimization   

P19   
## Gradient Descent    

Another way to solve \\(\mathbf{x}^∗\\)=argmin \\(F(\mathbf{x})\\) is the gradient descent method.   

![](./assets/08-7.png)   

How to find the optimal step size becomes a critical question.    


P20   
### step size adjustment    

![](./assets/08-8.png)   

优点：simple, Low overhead    



P21   
### Descent Directions   

The direction \\(\mathbf{d(x)}\\) is descending, if a sufficiently small step size \\(α\\) exists for:    

$$
F(\mathbf{x} )>F(\mathbf{x} +α\mathbf{d} (\mathbf{x} ))
$$

![](./assets/08-9.png)   


|  In other words, \\(−∇F(\mathbf{x} )\cdot \mathbf{d} (\mathbf{x} )>0\\)  |  
|---| 

> &#x2705;沿负梯度方向可以下降，但不一定是最好的方向。怎样判断一个方向是否可以下降？答：看与负梯度方向是否在同侧。   


P22    
With line search, we can use any search direction as long as it’s descending:    

$$
F(\mathbf{x} ^{(0)})>F(\mathbf{x} ^{(1)})>F(\mathbf{x} ^{(2)})>F(\mathbf{x} ^{(3)})>…
$$

![](./assets/08-10.png)   

P23   
## Descent Methods    

 - Gradient descent is a descent method, since:    

$$
\mathbf{d} (\mathbf{x} )=−∇F(\mathbf{x} )\quad \Rightarrow  \quad −∇F(\mathbf{x} )\cdot (−∇F(\mathbf{x} ))>0
$$

 - Newton’s method is also a descent method, if the Hessian is always positive definite:   

$$
\mathbf{d} (\mathbf{x} )=−(\frac{∂^2F(\mathbf{x} )}{∂\mathbf{x} ^2})^{−1}∇F(\mathbf{x} ) \quad \Rightarrow  \quad −∇F(\mathbf{x} )\cdot (−(\frac{∂^2F(\mathbf{x} )}{∂\mathbf{x} ^2})^{−1}∇F(\mathbf{x} ))>0
$$

> &#x2705;牛顿法不一定收敛，\\(\mathbf{H}\\)正定场景牛顿法一定收敛。   

 - **Any method using a positive definite matrix P to modify the gradient** yields a descent method:    

$$\mathbf{d} (\mathbf{x} )=−\mathbf{P} ^{−1}∇F(\mathbf{x} )
\quad \Rightarrow  \quad 
−∇F(\mathbf{x} )\cdot (−\mathbf{P} ^{−1}∇F(\mathbf{x} ))>0
$$





P24  
## A unified descent framework     


| Descent Methods   <br>  Initialize \\(x^{(0)}\\)    <br>   \\(\mathbf{x} ^{(k+1)}\longleftarrow \mathbf{x} ^{(k)}−α^{(k)}(\mathbf{P} ^{(k)})^{−1}∇F(\mathbf{x} ^{(k)})\\)     <br>  \\(\mathbf{x} ^∗\longleftarrow \mathbf{x} ^{(k+1)}\\)  |   
|----|  

[@] 以上内容截图

![](./assets/08-11.png)   



P25   
![](./assets/08-12.png)   


> &#x2705; 图形学中更关注 Total Cost. 让 P 更加接近 H，可以减少迭代数，让 P 更容易得到，减少迭代成本。   
Traction：物体表面上的力的密度，有点像压强   



P27   
### After-Class Reading    


Wang. 2016. Descent *Methods for Elastic Body Simulation
on the GPU*. TOG (SIGGRAPH Asia).    



P28  
# A Summary For the Day  


 - We can calculate the Hessian of the FEM elastic energy based on SVD derivatives.  

 - The goal of doing this is for implicit time integration. 

 - Fundamentally, the goal is to solve a nonlinear optimization.   
    - Gradient Descent, Newton’s method, and others can all be considered as descent methods.    
    - The key question is the matrix for calculating the search direction.    
    - We need both the per-iteration cost and the number of iterations to be small.   

> &#x2705; 模拟的公式通常都固定，很难有突破、瓶颈在于计算量、随着分辨率的提升，模拟的计算量几乎是无止境的。   

---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/
