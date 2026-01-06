# MPM

物质点法 (material point method, MPM)采用拉格朗日和欧拉双重描述，将物体离散为一组在空间网格中运动的质点。
- 质点携带了所有的物质信息，如质量、速度、应变和应力等，可很方便地跟踪材料的界面和引入与变形历史相关的材料模型。
- 质点在空间网格中运动，运动方程在空间网格上求解，避免了网格畸变问题，适合于分析特大变形及流动问题。



## 核心思想

拉格朗日视角 (粒子)：物质点携带密度、速度、应力等信息，随物质变形运动。  
欧拉视角 (背景网格)：划分计算域，用于计算空间导数和物理量更新。  
粒子-网格-粒子 (P-G-P)：信息通过物质点映射到网格节点，在网格上计算更新，再插值回物质点，完成一个时间步。   

## 主要特点与优势
融合拉格朗日与欧拉：兼具拉格朗日法的精确追踪物质界面能力和欧拉法的网格独立性，避免了有限元网格缠绕畸变问题。  
处理大变形：能有效模拟材料的超大变形、破碎、断裂等非线性问题。  
自动处理多体接触：物质点在网格内运动，自动处理多介质界面，无需复杂的碰撞检测。  
适用范围广：适用于高速碰撞、爆炸冲击、岩土动力学、流体与固体相互作用等复杂问题。    

但 MPM 在精度上存在劣势。   

## 基本步骤（一个时间步）  
粒子到网格 (P2G)：将物质点信息（如质量、动量）通过插值函数映射到背景网格节点。  
网格计算：在背景网格上，根据控制方程（如动量守恒）计算节点力、加速度等。  
网格到粒子 (G2P)：将网格上的计算结果（如速度、应力）通过插值函数传回物质点。  
更新粒子：更新物质点的位置、速度和应力状态。  
（可选）丢弃网格：根据需要重新划分或更新背景网格。   


> &#x1F50E; Deborah Sulsky, Shi-Jian Zhou, and Howard L Schreyer.
Application of a particle-in-cell method to solid mechanics.

# MLS-MPM 移动最小二乘物质点法


传统MPM将物体离散为携带各类拉格朗日量的粒子，包括位置 \\( \mathbf{x}_p \\)、速度 \\( \mathbf{v}_p \\) 和变形梯度 \\( \mathbf{F}_p \\)。随后通过粒子到欧拉网格的传递操作与网格到粒子的传递操作更新粒子状态。  
在该方法中，在时间步 \\( t^n \\) 到 \\( t^{n+1} \\) 的更新过程中，使用 \\( \nabla N_i(\mathbf{x}_p) \\)（三维二次B样条核函数需迭代27次）计算网格动量，其中 \\( N_i(\mathbf{x}_p) \\) 是在第 \\( i \\) 个网格上定义、并于粒子位置 \\( \mathbf{x}_p \\) 处取值的B样条核函数。  
如果场景包含上万个点，使用传统MPM方法模拟这些点将非常耗时。而MLS-MPM相较于传统MPM，加速模拟的同时，显著降低了计算成本。作为一种混合欧拉-拉格朗日方法，它通过以下方程更新网格动量：

$$
\frac{m_i^{n+1} \hat{\mathbf{v}}_i^{n+1} - m_i^n \mathbf{v}_i^n}{\Delta t} = m_i^n \mathbf{g} + \mathbf{f}_i^n,
$$

其中，\\( m_i^n \\) 是第 \\( i \\) 个网格的质量，\\( \mathbf{v}_i^n \\) 是第 \\( i \\) 个网格的速度，\\( \mathbf{g} \\) 为重力加速度，\\( \Delta t \\) 是时间步长。此外：

$$
\mathbf{f}_i^n = -\frac{\partial E}{\partial \mathbf{x}_i} = -\sum_p N_i(\mathbf{x}_p^n) V_p^0 \mathbf{W}_p^{-1} \frac{\partial \Psi}{\partial \mathbf{F}}(\mathbf{F}_p^n) \mathbf{F}_p^{nT} (\mathbf{x}_i^n - \mathbf{x}_p^n),
$$

这里 \\( i \\) 与 \\( p \\) 分别表示欧拉网格场与拉格朗日粒子场。

$$
E = \sum_p V_p^0 \Psi_p(\mathbf{F}_p)
$$

其中 \\( V_p^0 \\) 为粒子初始体积，\\( \Psi_p \\) 是能量密度函数；\\( \mathbf{W}_p \\) 是 \\( \mathbf{x}_p \\) 的矩矩阵，对于二次 \\( N_i(x) \\) 有 \\( \mathbf{W}_p = \frac{1}{4} \Delta x^2 \\)，对于三次核函数则为 \\( \frac{1}{3} \Delta x^2 \\)；\\( \mathbf{F}_p \\) 是从拉格朗日视角观察的粒子变形梯度，通过 \\( \mathbf{F}_p^{n+1} = (\mathbf{I} + \Delta t \mathbf{C}_p^{n+1}) \mathbf{F}_p^n \\) 更新，其中 \\( \mathbf{C}_p^{n+1} \\) 是粒子 \\( p \\) 的仿射矩阵。


> &#x1F50E; Yuanming Hu, Yu Fang, Ziheng Ge, Ziyin Qu, Yixin Zhu, Andre Pradhana, and Chenfanfu Jiang. 2018. A moving least squares material point method with displacement discontinuity and two-way rigid body coupling.


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/