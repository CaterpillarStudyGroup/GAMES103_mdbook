# 刚体对外力的响应

虽然刚体受到的力都是作用在刚体上的某个点上。但受力点不能独立的响应这个力。而是要让刚体作为整体来响应这个力。  
即，刚体的质心的全局位置（世界坐标系）和全局旋转（世界坐标系）。  
因此，刚体在力的作用下会发生旋转和平移。  

![](../assets/03-1.png)     

## 平移

刚体受力后的平移响应与粒子相似。  

1. 当刚体同时受到多个力时，通过相加计算出合力。
2. 连续形式与离散形式下的速度、位置更新公式也相同

![](../assets/03-3.png)     

不同的是，在刚体仿真中，质量 \\(M\\) 可以是个对角矩阵或实数

## 旋转

当受到的所有力都是作用于质心或者均匀作用于每个点(例如重力)时，刚体不会发生旋转。  
因此这里只分析力的作用点不在质心时的场景。  
力造成物体运动的趋势。 Torque（力矩）造成物体旋转的趋势。为了计算刚体在下一时刻的旋转状态，需要把力转化力矩。
> &#x2705; 力转化为力矩，不是物理性质上的转化，而是数学形式上的转化。把力用力矩的形式表达，用于计算它对旋转产生的影响。  
> inertia、torque等概念，请戳这里[link](./supplementary.md)

参考刚体平移的离散积分过程，可以推导出刚体旋转的更新法则：

|    |Translational (linear)|Rotational (Angular)|
|---|---|---|
|Updafe|![](../assets/03-23.png)   |![](../assets/03-24.png)   |
|states| Velocity \\(\mathbf{v}\\) <br> Position \\(\mathbf{x}\\)|Angular velocity \\(\mathbf{ω} \\)<br>   Quaternion \\(\mathbf{q}\\) |
| Physical Quantities |Mass \\(\mathbf{M}\\) <br> Force \\(\mathbf{f}\\) | Inertia \\(\mathbf{I} \\) <br> Torque \\(\mathbf{τ} \\) |


> &#x2705;  平移： \\(加速度 = \frac{力}{质量}\\) ，旋转： \\(加速度 =\frac{力矩}{\text{Inertia}}\\)   
> &#x2705;  \\(q\\)是四元数，代表物体的旋转状态   
> &#x2705;  \\(q_1\times q_2\\)不是叉乘，而是四元数普通乘法    
> &#x2705;  \\(\begin{bmatrix}
  0 & \frac{\bigtriangleup t}{2}  & w^{(1)}
\end{bmatrix}\\)是一个四元数，0为实部，后面为虚部   
> &#x2757;  算完\\(q^{[1]}\\)的之后要对它 Normalize     
> &#x1F50E; 由\\(q^{[0]}\\)到\\(q^{[1]}\\)的更新公式的推导过程见Affer Class Reading（Appendix B）   

![](../assets/03-20.png)    

P30 
# 总结       

![](../assets/03-27.png)  
![](../assets/04-1.png)     
