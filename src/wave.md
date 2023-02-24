
P1   
## Fluid Effects    


Unlike other bodies, Fluids exhibit highly volatile behaviors. As a result, it’s difficult to come up with a single, efficient way for simulating all of fluid effects.     



P3   
## Two Types of Simulation Approaches  


|  ![](./assets/10-1.png)   |  ![](./assets/10-2.png)  |  
|---|----|
| Lagrangian Approach <br>(dynamic particles or mesh)<br> Node movement carries physical quantities (mass, velocity, …). |  Eulerian Approach <br> (static grid or mesh) <br> Grid/Mesh doesn’t move.  Stored physical quantities change.  |
  

> &#x2705; 左：无 Grid. 物理量附加在粒子上，粒子运动时更新自身物理量。  
右：固定 Grid. 物理量固定在 Grid 上。粒子运动后统一新格子的物理量。   


P4   
## A Height Field Model   


P5   
## Height Field    

![](./assets/10-3.png)    


> &#x2705; 水流的方向， < 0 则高往低， > 0 则低往高。 


P6   
## Height Field   

![](./assets/10-4.png) 


> &#x2705;  \\(h(x)u(x)\\): 单位时间内流过x线的水量。     
\\(d(h(x)u(x))\\) 单位时间内区域 \\([x \quad x+dx]\\) 的水量变化、    
\\(d(h(x)u(x))1/x\\) 单位时间内区域区 \\([x \quad x+dx]\\) 的水位高度变化    
速度场第一项：当水在流动时，速度应该跟水一起流动，下节课再讲。第三项是外力，当前也不考虑。  



P7   
## Height Field   

![](./assets/10-5.png)    


> &#x2705;  在短时间内、速度变化由左右压强差决定。  


P8   
## Height Field

Ignoring advection and external acceleration, we get a simple form:   

$$
\begin{matrix}
\frac{du(x)}{dt}=−\frac{1}{ρ} \frac{dP(x)}{dx} \quad \quad & ρ: \text{density} \quad \quad & P(x):\text{pressure}
\end{matrix}
$$


![](./assets/10-6.png)   



P9   
## Shallow Wave Equation   

We now have two equations:   

![](./assets/10-7.png) 

We can then eliminate \\(u\\) and formulate the shallow wave equation:    

| $$\frac{d^2ℎ}{dt^2} =\frac{ℎ}{ρ} \frac{d^2P}{dx^2} $$ |
|----|  


> &#x2705;  为什么叫 Shallow Wave, 因为该算法假设水波很小，因此 \\(dh / dx\\) 可忽略不计。    
公式化简的目的：不需要关心速度场、仅关注高度场就可以，但引擎无法直接处理微分程，因此要离散化开求解。   



P10  
## Discretization


We discretize a continuous height field into a discrete set of height columns.    

![](./assets/10-8.png)  



P11   

## Finite Differencing   

The idea of finite differencing is to use the difference to approximate the derivative.     

![](./assets/10-9.png)  

$$
f(t_0+∆t)=f(t_0)+∆t\frac{df(t_0)}{dt} +\frac{∆t^2}{2} \frac{d^2f(t_0)}{dt^2} +…
$$

Forward differencing (first-order)   

| $$\frac{df(t_0)}{dt} ≈\frac{f(t_0+∆t)−f(t_0)}{∆t}$$ | 
|---|




![](./assets/10-10.png)  

$$
f(t_0−∆t)=f(t_0)−∆t\frac{df(t_0)}{dt}+\frac{∆t^2}{2}\frac{d^2f(t_0)}{dt^2} +…
$$

Backward differencing (first-order)     

| $$ \frac{df(t_0)}{dt}≈\frac{f(t_0)−f(t_0−∆t)}{∆t} $$ | 
|---|


P12   
## Finite Differencing

The idea of finite differencing is to use the difference to approximate the derivative.    

![](./assets/10-111.png)


Central differencing (second-order)   

| $$ \frac{df(t_0)}{dt}≈\frac{f(t_0+∆t)−f(t_0−∆t)}{2∆t} $$ | 
|---|



P13   
## Second-Order Derivatives   

We apply central differencing twice to estimate \\(d^2ℎ_i/dt^2\\).    

$$
\begin{matrix}
 \frac{dℎ_i(t_0+0.5∆t)}{dt}≈\frac{ℎ_i(t_0+∆t)−ℎ_i(t_0)}{∆t}  \quad\quad& \frac{dℎ_i(t_0−0.5∆t)}{dt}≈\frac{ℎ_i(t_0)−ℎ_i(t_0−∆t)}{∆t} 
\end{matrix}
$$

| $$\frac{d^2ℎ_i(t_0)}{dt^2}≈\frac{\frac{dℎ_i(t_0+0.5∆t)}{dt}−\frac{dℎ_i(t_0−0.5∆t)}{dt} }{∆t} ≈\frac{ℎ_i(t_0+∆t)+ℎ_i(t_0−∆t)−2ℎ_i(t_0)}{∆t^2}$$ |
|---|


![](./assets/10-12.png)   


> &#x2705;  先用 central difference 求出两个中点的一阶导数，再基于此计算 \\(to\\) 处的二阶导。这种操作又称为一维Laplace 算子。    



P14    
## Second-Order Derivatives   

Similarly, we apply central differencing twice to estimate \\(d^2P/dx^2\\).      

$$
\begin{matrix}
 \frac{dP_{i+0.5}}{dt} ≈\frac{P_{i+1}−P_i}{∆x} \quad\quad & \frac{dP_{i−0.5}}{dx} ≈\frac{P_i−P_{i−1}}{∆x} 
\end{matrix}
$$


|  $$\frac{d^2P_i}{dx^2}≈\frac{\frac{dP_{i+0.5}}{dx}−\frac{dP_{i−0.5}}{dx}}{∆x} ≈\frac{P_{i+1}+P_{i−1}−2P_i}{∆x^2}$$ |
|---|   

![](./assets/10-13.png)   




P15   
## Discretized Shallow Wave Equation    

We can now discretize the shallow wave equation \\(\frac{d^2ℎ}{dt^2}=\frac{ℎ}{ρ}\frac{d^2P}{dx^2}\\).     

 
> \\(\begin{matrix}\\
 \frac{d^2ℎ_i(t_0)}{dt^2}≈\frac{ℎ_i(t_0+∆t)+ℎ_i(t_0−∆t)−2ℎ_i(t_0)}{∆t^2}\quad  &\frac{d^2P_i}{dx^2 }≈\frac{P_{i+1}+P_{i−1}−2P_i}{∆x^2}\\\\
\end{matrix}\\)

> \\(\Rightarrow \frac{ℎ_i(t_0+∆t)+ℎ_i(t_0−∆t)−2ℎ_i(t_0)}{∆t^2}=\frac{ℎ_i}{ρ} (\frac{P_{i+1}+P_{i−1}−2P_i}{∆x^2})\\)


>\\(\Rightarrow ℎ_i(t_0+∆t)=2ℎ_i(t_0)−ℎ_i(t_0−∆t)+\frac{∆t^2ℎ_i}{∆x^2ρ}(P_{i+1}+P_{i−1}−2P_i)\\)


> &#x2705;  更新目标：下一个时刻的水柱的高度，即 \\(hi(t_0 + ∆t)\\)    
但按此公式模拟可能出现水的体积变多或变少的问题。   



P16    
## Volume Preservation     

We want the volume to stay the same. Suppose that \\(\sum ℎ_i(t)=\sum ℎ_i(t−∆t)=V\\). But,    

$$
ℎ_i(t_0+∆t)=2ℎ_i(t_0)−ℎ_i(t_0−∆t)+\frac{∆t^2ℎ_i}{∆x^2ρ}(P_{i+1}+P_{i−1}−2P_i)
$$


![](./assets/10-14.png)   



> &#x2705;  体积会变大还是变小，取决于桔色项，但很难保证这一项是0.   



P17    
## Volume Preservation – Solution 1    


![](./assets/10-15.png)    


> &#x2705;  保证 \\(h_i\\) 和 \\(h_{i+1}\\)的交换的水量相等、因此保体积   



P18  
## After-Class Reading    

Kass and Miller. 1990. *Rapid, Stable Fluid Dynamics for Computer Graphics*. Computer Graphics.    





P19   
## Volume Preservation – Solution 2

An easier way to preserve volume is to **simply assume** \\(h_i\\) in the right term is constant.     

![](./assets/10-16.png)    




P20   
## Pressure    

![](./assets/10-17.png) 




P21   
## Viscosity   


Like damping, viscosity tries to slow down the waves. 

![](./assets/10-18-1.png) 


> &#x2705;  Viscosity: 粘滞，相当于流体的阻尼。   



P22   
## Algorithm  


> $$\text{A Shallow Wave Simulator}$$
For every cell \\(i\\)
$$ℎ_i^{new}←ℎ_i+β(ℎ_i−ℎ_i^{old})\\\\
ℎ_i^{new}←ℎ_i^{new}+α(ℎ_{i−1}−ℎ_i)\\\\
ℎ_i^{new} ←ℎ_i^{new}+α(ℎ_{i+1}−ℎ_i)\\\\$$
For every cell \\(i\\)
$$ℎ_i^{old}←ℎ_i\\\\    
ℎ_i←ℎ_i^{new}$$






P23  
## Boundary Conditions   

![](./assets/10-19-1.png) 

A Dirichlet boundary assumes that the boundary height \\(H_{i+1}\\) is constant.  It’s considered as an open boundary.    

$$
ℎ_{i+1}−ℎ_i+ℎ_{i−1}−ℎ_i=H_{i+1}−ℎ_i+ℎ_{i−1}−ℎ_i
$$


![](./assets/10-19-2.png) 

A Neumann boundary specifies the boundary derivatives.  For example, a zero-derivative boundary means \\(ℎ_{i+1}≡ℎ_i\\).  It’s considered as a closed boundary.   

$$
ℎ_{i+1}−ℎ_i+ℎ_{i−1}−ℎ_i=ℎ_{i−1}−ℎ_i
$$


> &#x2705;  这种方法用于模拟开放的水面，例如大海的区域、假设被模拟的区域外是静止的水面、高度为常数，(Dirichlet)    
Neuman 用于模拟有边界水域，例如池堂、假设边界上没有水流交换。   



P24   
## Algorithm with Neumann Boundaries


> $$\text{A Shallow Wave Simulator}$$    
For every cell \\(i\\)   
$$ℎ_i^{new}←ℎ_i+β(ℎ_i−ℎ_i^{old})\\\\\text{If } ℎ_{i−1}\text{ exists, then  }ℎ_i^{new}←ℎ_i^{new}+α(ℎ_{i−1}−ℎ_i)\\\\ \text{If } ℎ_{i+1} \text{ exists,  then } ℎ_i^{new}←ℎ_i^{new}+α(ℎ_{i+1}−ℎ_i)$$
For every cell \\(i\\)    
$$ℎ_i^{old}←ℎ_i\\\\ℎ_i←ℎ_i^{new}  $$




P25   
## Algorithm with Neumann Boundaries   

Extending the simulator to 3D is also straightforward.   

> $$\text{A Shallow Wave Simulator}$$      
For every cell \\(i, j\\)    
$$ℎ_{i,j}^{new}←ℎ_{i,j}+β(ℎ_{i,j}−ℎ_{i,j}^{old})\\\\\text{If } ℎ_{i−1,j} \text{ exists, then  } ℎ_{i,j}^{new}←ℎ_{i,j}^{new}+α(ℎ_{i−1,j}−ℎ_{i,j})\\\\ \text{If } ℎ_{i+1,j} \text{ exists, then  } ℎ_{i,j}^{new}←ℎ_{i,j}^{new}+α(ℎ_{i+1,j}−ℎ_{i,j})\\\\  \text{If } ℎ_{i,j−1} \text{ exists, then  } ℎ_{i,j}^{new} ←ℎ_{i,j}^{new}+α(ℎ_{i,j−1}−ℎ_{i,j})\\\\ \text{If } ℎ_{i,j+1} \text{ exists, then  } ℎ_{i,j}^{new}←ℎ_{i,j}^{new}+α(ℎ_{i,j+1}−ℎ_{i,j})$$
For every cell \\(i, j\\)    
$$ℎ_{i,j}^{old}←ℎ_{i,j}\\\\ℎ_{i,j}←ℎ_{i,j}^{new}$$




P26   
## Two-Way Coupling    

The coupling between a solid and a liquid should be two-way, i.e., liquid->solid and solid->liquid.    

![](./assets/10-20.png)   


> &#x2705; 水和水中的物体相互作用，物体可以是刚体、弹性体能各种类型的物体。    
水→物体：浮力、物体→水，会把这个水柱的水排出去，此处只讲“物体 → 水” 部分   



P27   
## Two-Way Coupling

The coupling between solid and water should be two-way, i.e., water>solid and solid- >water.     

The key question is how to expel water out of the gray cell regions???    

![](./assets/10-21.png)    



P28   
## Virtual Height    

The idea is to set up a virtual height \\(v_i\\), so that  \\(ℎ_i^\text{real_new}=ℎ_i−e_i\\).    

$$
ℎ_i−e_i=ℎ_i+β(ℎ_i−ℎ_i^{old})+α(v_{i+1}+ℎ_{i+1}+ℎ_{i−1}−2v_i−2{ℎ_i})=ℎ_i^{new}+α(v_{i+1}−2v_i)
$$

$$
ℎ_{i+1}−e_{i+1}=ℎ_{i+1}+β(ℎ_{i+1}−ℎ_{i+1}^{old})+α(ℎ_{i+2}+v_i+ℎ_i−2v_{i+1}−2ℎ_{i+1})=ℎ_{i+1}^{new}+α(v_i−2v_{i+1})
$$

![](./assets/10-22.png)    


> &#x2705; 在要排的水柱上面增加一个虚拟的高度，然后正常模拟，关键是求出要加多少虚拟高度，能正好达到排出那么多水的效果。   



P29   
## Poisson’s Equation    

The outcome is Poisson’s equation, with \\(v_i\\) and \\(v_{i+1}\\) being unknowns.    

$$
2v_i−v_{i+1}=\frac{1}{α}(ℎ_i^{new}−ℎ_i+e_i)=b_i
$$

$$
−v_i+2v_{i+1}=\frac{1}{α}(ℎ_{i+1}^{new}−ℎ_{i+1}+e_{i+1})=b_{i+1}
$$


![](./assets/10-23.png)    



P30   
## Poisson’s Equation   

The outcome is Poisson’s equation, with \\(v_i\\) and \\(v_{i+1}\\) being unknowns.    

![](./assets/10-24.png)    


> &#x2705; 没听懂，似乎是为了让公式统一方便计算   



P31  
## Algorithm with Coupling    

![](./assets/10-25.png)    


> &#x2705; \\(\gamma \\) 的作用：本算法显式积分，不稳定、\\(\gamma \\) 会让水波小很多。    



P32   
## Rigid Body Update   


We estimate the floating force by the actual water expelled in every column.      

![](./assets/10-26.png)    

$$
f_i=ρg∆x(ℎ_i−ℎ_i^{new})
$$

Or in 3D,   

$$
f_{i,j}=ρg∆A(ℎ_{i,j}−ℎ_{i,j}^{new})
$$


> &#x2705; 阿基采得定律：物体受到的浮力 = 排出去的水的重量；同时要考虑旋转和力矩。    



P33   
## A Summary For the Day

 - The shallow wave model simulates waves over a height field.    

 - It’s based on a lot of simplification. We will discuss what fluid dynamics really looks like without simplification.    
 
 - The strength of the shallow wave model is its **simplicity** and **efficiency**. It can easily simulate water-solid coupling too.  
 
 - See Lab 4 for more details.    
