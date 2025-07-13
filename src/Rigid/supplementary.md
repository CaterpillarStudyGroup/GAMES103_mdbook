# 力与力矩

## 力矩 torque \\(\mathbf{τ} \\) 

A torque is the rotational equivalent of a force. It describes the rotational <u>tendency</u> caused by a force.    

> &#x2705; Torque：力矩，造成物体旋转的趋势。类比于Force：力，造成物体运动的趋势。   

![](../assets/04-2.png)     

> &#x2705; \\(\mathbf{Rr} _i\\)：当前状态下质心到作用点的向量 

\\(\mathbf{τ} _i\\) is perpendicular to both vectors: \\(\mathbf{Rr} _i\\) and \\(\mathbf{f} _i\\).    

> &#x2705; 力矩的方向决定了旋转轴的方向，由叉差乘得到   

\\(\mathbf{τ} _i\\) is porportional to ||\\(\mathbf{Rr} _i\\)|| and ||\\(\mathbf{f} _i\\)||.    


\\(\mathbf{τ} _i\\) is porportional to \\(\sin \theta\\).     
(\\(\theta\\)  is the angle between two vectors.)

> &#x2705; 力矩的大小决定旋转的快慢。 

|\\(\mathbf{τ} _i\longleftarrow (\mathbf{Rr} _i)\times \mathbf{f} _i\\)|   
|----|

![](./assets/03-22.png) 

P6   

## inertia tensor

Similar to mass, an inertia tensor describes the resistance to rotational tendency caused by torque. But different from mass, it’s not a constant.    

> &#x2705; inertia 也与自身的状态相关

![](./assets/04-3.png)     

Which side receives greater resistance?     

> &#x2705; 两图的力矩大小相同，但产生的旋转不同   
inertia 看作是对运动的抵抗，其效果与力矩的方向有关，因此不是常数  

P7   

It’s a matrix! The mass inverse is the resistance (just like mass).    

> &#x2705; 用于旋转的质量不再是实数，而是矩阵，称为 Inertia 矩阵，用 \\(\mathbf{I}\\) 来标记 Inertia 矩阵，其中 \\(\mathbf{I}_{ref}\\)为参考状态，\\(\mathbf{I}\\) 为当前状态，\\(\mathbf{I}\\) 是 \\(3\times 3\\) 矩阵。  

|reference state|current state|
|---|---|
|![](../assets/04-4.png)| ![](../assets/04-5.png)   |
|\\(\mathbf{I} _{\mathbf{ref} }=\sum m_i(\mathbf{r} _i^\mathbf{T} \mathbf{r} _i\mathbf{1} −\mathbf{r} _i\mathbf{r} _i^\mathbf{T} )\\)<br>\\(\mathbf{1}\\)  is the 3-by-3 identity.|\\(\mathbf{I} =\sum m_i(\mathbf{r} _i^\mathbf{T}\mathbf{R}  ^\mathbf{T}\mathbf{Rr}  _i\mathbf{1} −\mathbf{Rr} _i\mathbf{r} _i^\mathbf{T} \mathbf{R^T} )\\)  <br> \\(\quad=\sum m_i(\mathbf{Rr} _i^\mathbf{T}\mathbf{r}  _i\mathbf{1R}  ^\mathbf{T} −\mathbf{Rr} _i\mathbf{r} _i^\mathbf{T} \mathbf{R^T} )\\) <br> \\(\quad=\sum m_i\mathbf{R}(\mathbf{r}_i^\mathbf{T}\mathbf{r}_i\mathbf{1}−\mathbf{r}_i\mathbf{r}_i^\mathbf{T} ) \mathbf{R^T}\\)   <br> \\(\quad=\mathbf{RI _{ref}R^T}\\)|

> &#x2705; 不需要每次都根据当前状态计算，而是基于一个已经算好的ref状态的 inertia快速得出。  


P33
# After-Class Reading (Before Collision)

P35  

<https://graphics.pixar.com/pbm2001>     

> &#x2705; 建议读其中的Rigid Body Dynamics部分    

---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/
