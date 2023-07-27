P2   

## Topics for the Day   

 - The linear finite element method (FEM)
 - The finite volume method (FVM)
 - Hyperelastic models




P3   
# Linear Finite Element Method    

P4  
## The Linear FEM Assumption   

In a nutshell, linear FEM assumes that for any point \\(\mathbf{X}\\) in the reference triangle, its deformed correspondence is: \\(\mathbf{x=FX+c}\\).    

![](./assets/07-1.png)    


For any vector between two points, we can use F to convert it from reference to deformed:    
$$
\mathbf{x} _{ba}=\mathbf{x} _b−\mathbf{x} _a=\mathbf{FX} _b+\mathbf{c} −\mathbf{FX} _a−\mathbf{c} =\mathbf{FX} _{ba}.
$$


> &#x2705; reference triangle：三角形处于没有发生形变的静止的状态。   
假设：三角形的形变是均匀的    
\\(\mathbf{X}\\)和\\(\mathbf{x}\\)可以分别是 reference 和 deformed 三角形的顶点或内部点，公式都同样适用。  


P5   
## Deformation Gradient    

Therefore, we can calculate the deformation gradient by edge vectors.      

![](./assets/07-2.png)    


**Problem:** \\(\mathbf{F}\\) **is related to deformation, but it contains rotation**.     


> &#x2705; 期望\\(\mathbf{F}\\)只包含形变量、不包含平移和旋转、因为刚体运动不应该有形变，所以要把形变提取出来。    

> &#x2705;平移已经在\\(\mathbf{c}\\)里面了，所以只需考虑旋转。   



P6  
## Green Strain    

Ideally, we need a tensor to describe shape deformation only.  Recall that SVD gives \\(\mathbf{F=UDV^T}\\), where only \\(\mathbf{V^T}\\) and \\(\mathbf{D}\\) are relevant to deformation.     

![](./assets/07-3.png)    

So we get rid of \\(\mathbf{U}\\) as: \\(\mathbf{G} =\frac{1}{2} (\mathbf{F^TF−I} )=\frac{1}{2} (\mathbf{VD} ^2\mathbf{V} ^\mathbf{T} −\mathbf{I} )=\begin{bmatrix}
 \varepsilon _{uu} & \varepsilon _{uv}\\\\
\varepsilon _{uv} & \varepsilon _{vv}
\end{bmatrix}\\), *Green strain*.


 - If no deformation, \\(\mathbf{G=0}\\); if deformation increases,  ||\\(\mathbf{G}\\)|| increases.    
 - Three deformation modes: \\(\varepsilon _{uu}\\), \\(\varepsilon _{vv}\\) and \\(\varepsilon _{uv}\\).
 - \\(\mathbf{G}\\) is <u>rotation invariant</u>: if additional rotation \\(\mathbf{R}\\), then deformation gradient is \\(\mathbf{RF}\\) but green strain is the same: \\(\mathbf{G} =\frac{1}{2} (\mathbf{F^TR^TRF−I} )=\frac{1}{2} (\mathbf{VD} ^2\mathbf{V} ^\mathbf{T} −\mathbf{I} )\\).    



> &#x2705; \\(\mathbf{V^T}\\) 看上去是旋转、实际上是为了确定形变的方向、 \\(\mathbf{U}\\) 才是真正的旋转     
目的：把\\(\mathbf{F}\\)中的\\(\mathbf{U}\\)去掉、可以先做 \\(\mathbf{SVD}\\) 分解再把\\(\mathbf{U}\\)去掉。但本文使用了更简单的方法     
\\(\mathbf{G}\\) 是一个描述物体形变的有无和大小矩阵，且与关旋转     




P7   
## Strain Energy Density Function    


Let \\(\mathbf{G}\\) be the the green strain describing deformation. We consider the **energy density** per reference area as: \\(W (\mathbf{G})\\).    

![](./assets/07-4.png)    

![](./assets/07-5.png)    

![](./assets/07-6.png)    


> &#x2705;  \\(A^{ref}\\) 为 reference status 下三角形的面积     
StVK 在力学中不常用，但在图形学中很常用、原因是简单    
S 是一个类似于力的物理量。   

> &#x2705;用形变程度来定义能量。   
\\(W\\)代表单位面积上的能量，因此称为能量密度。   
总能量为单位能量\\(\mathbf{X}\\)面积.    


P8  
## Forces   

Given everything we have, we can now calculate the forces.    
![](./assets/07-7.png)    


> &#x2705; 绿色部分是上一页S中的内容、灰色部分将在下一页推导。  



P9   
## Forces 

Recall that,    

![](./assets/07-8.png)    


By definition,    
$$
\mathbf{G} =\frac{1}{2} (\mathbf{F^TF−I} )=\begin{bmatrix}
 \frac{1}{2}(a\mathbf{x} _{10}+c\mathbf{x} _{20})^\mathbf{T} (a\mathbf{x} _{10}+c\mathbf{x} _{20})−\frac{1}{2}  & \frac{1}{2}(a\mathbf{x} _{10}+c\mathbf{x} _{20})^\mathbf{T} (b\mathbf{x} _{10}+d\mathbf{x} _{20})\\\\
 \frac{1}{2}(a\mathbf{x} _{10}+c\mathbf{x} _{20})^\mathbf{T} (b\mathbf{x} _{10}+d\mathbf{x} _{20})  & \frac{1}{2}(b\mathbf{x} _{10}+d\mathbf{x} _{20})^\mathbf{T} (b\mathbf{x} _{10}+d\mathbf{x} _{20})−\frac{1}{2}
\end{bmatrix}
$$

So:

$$
\frac{∂\varepsilon _{uu}}{∂\mathbf{x} _1}=a(a\mathbf{x} _{10}+c\mathbf{x} _{20})^\mathbf{T} 
\quad\quad
\frac{∂\varepsilon _{vv}}{∂\mathbf{x} _1}=b(b\mathbf{x} _{10}+d\mathbf{x} _{20})^\mathbf{T} 
\quad\quad
\frac{∂\varepsilon _{uv}}{∂\mathbf{x} _1}=\frac{1}{2} a(b\mathbf{x} _{10}+d\mathbf{x} _{20})^\mathbf{T} +\frac{1}{2}  b(a\mathbf{x} _{10}+c\mathbf{x} _{20})^\mathbf{T} 
$$

$$
\frac{∂\varepsilon _{uu}}{∂\mathbf{x} _2}=c(a\mathbf{x} _{10}+c\mathbf{x} _{20})^\mathbf{T} 
\quad\quad
\frac{∂\varepsilon _{vv}}{∂\mathbf{x} _2}=d(b\mathbf{x} _{10}+d\mathbf{x} _{20})^\mathbf{T} 
\quad\quad
\frac{∂\varepsilon _{uv}}{∂\mathbf{x} _2}=\frac{1}{2} c(b\mathbf{x} _{10}+d\mathbf{x} _{20})^\mathbf{T} +\frac{1}{2}  d(a\mathbf{x} _{10}+c\mathbf{x} _{20})^\mathbf{T} 
$$

> &#x2705;\\(\mathbf{F}\\)不是力，是deformation gradient．   
\\(\mathbf{x}\\)为current边的矩阵，\\(\mathbf{r}\\)为reference边的矩阵。这个推导方法从定义出来，过程简单，但很容易出错。    



P10     
## Forces 

![](./assets/07-9.png)    


> &#x2705; 把 P9 代入 P8 得到 P10       

> &#x2705;用矩阵来简化计算   
力是形变施加到顶点上的力   



P11     
## Forces 


In conclusion, we have:   

$$
\mathbf{f} _1=−A^{\mathrm{ref} }\mathbf{FS} \begin{bmatrix}
 a\\\\
b
\end{bmatrix}  \quad\quad \mathbf{f} _2=−A^{\mathrm{ref} }\mathbf{FS} \begin{bmatrix}
 c\\\\
d
\end{bmatrix}
$$

$$
\begin{bmatrix}
 \mathbf{f} _1 &\mathbf{f} _2
\end{bmatrix}= − A ^{\mathrm{ref} }\mathbf{FS} \begin{bmatrix}
 \mathbf{X} _{10} & \mathbf{X} _{20}
\end{bmatrix}^\mathbf{−T} 
$$


> &#x2705; \\(f_0=-f_1-f_2\\)   


P12   
## Implementations   

 - More details?
    - Volino et al. 2009. *A simple approach to nonlinear tensile stiffness for accurate cloth simulation*. TOG    
    - Only talks about cloth (2D reference -> 3D deformation)    

 - What about tetrahedron (3D reference -> 3D deformation)?   
    - Same idea, but everything is now in 3D.   
    - Deformation gradient \\(\mathbf{F} \in \mathbf{R} ^{3×3}\\)   
    - Green strain \\(\mathbf{G} \in \mathbf{R} ^{3×3}\\)   
    - Stress tensor \\(\mathbf{S} \in \mathbf{R} ^{3×3}\\)   
    - Forces \\(\mathbf{F}_i \in \mathbf{R} ^3\\)    



P13   
# Finite Volume Method    

> &#x2705;在线性场景下，FEM和FVM本质上等价的。    



P14   
## Traction and Stress    

First, let’s consider traction **t**: the internal force per unit length (area).

![](./assets/07-10.png)    

Total interface force:    

$$
f\mathbf{} =\oint _L \mathbf{t} dl
$$

Stress tensor \\(\mathbf{σ} \\) (interface normal -> traction):

$$
\mathbf{t=σn} 
$$

So,    

$$
\mathbf{f} =\oint_{L}  \mathbf{σn} dl
$$


> &#x2705; 两个弹性体被界面 \\(L\\) 分开、求 \\(L\\) 上的力、   
\\(\mathbf{t},L\\) 上的单位面积/长度上的力、   
\\(\mathbf{σ}\\) 一个矩阵    



P15   
## The Finite Volume Method   


FVM considers force calculation in an integration perspective, not a differentiation perspective.     

![](./assets/07-11.png)    

Force contributed by an element:    

$$
\mathbf{f}_0 =\oint _L \mathbf{σn} dl
$$

Since \\(\mathbf{σ}\\) is constant within the element,     

$$
\oint_L \mathbf{σn} dl + \oint_{L_{20}} \mathbf{σn} dl+\oint_{L_{10}}\mathbf{σn} dl=0
$$

(Divergence Theorem)   

We know the force is:   



$$
\mathbf{f}_0 = - \oint _ {L _{20}} \mathbf{σn} _ {20} dl -  \oint _ {L _{10}} \mathbf{σn} _ {10} dl = - \mathbf{σ}(\frac{||\mathbf{X} _ {20}||}{2}\mathbf{n} _ {20}+ \frac{||\mathbf{X} _ {20}||}{2}\mathbf{n} _ {10})
$$


> &#x2705;  \\(\mathbf{X}_0\\)是顶点\\(\mathbf{X}_1\\)附近邻域面积上的力。    
\\(\mathbf{X}_0\\)上的力是邻域面边界\\(L\\)上的力的积分、不考虑边界内部的力，因为认为内力为0。   
仅看其中一个三角形、假设曲线经过 \\(\mathbf{X}_0\mathbf{X}_1\\)和 \\(\mathbf{X}_0\mathbf{X}_2\\)的中点。因为三角形的力对三个顶点是平均的。    
对于封闭曲线， \\(\int _n=0\\)，因此 \\(\sigma \int _n=0\\)    
三维场景是对四面体的四个面积分。  
每个三角形的 stress 都不同、同一个三角形内部 stress 是常数。  



P16   
### The Finite Volume Method   


In 3D, FVM works in the same way.    

![](./assets/07-12.png)    


Force:


$$
\begin{array}{l} 
 \mathbf{f} _ 0 = −\oint _ Ω \mathbf{σn} dA=−\mathbf{σ} (\frac{A _ {012}}{3}\mathbf{n} _ {012} + \frac{A _ {023}}{3}\mathbf{n} _ {023} + \frac{A _ {031}}{3}\mathbf{n} _ {031})\\\\
 =−\frac{σ}{3}(\frac{||\mathbf{x} _ {10} \times \mathbf{x} _ {20}||}{2} \frac{\mathbf{x} _ {10} × \mathbf{x} _ {20}}{||\mathbf{x} _ {10} × \mathbf{x} _ {20}||} + \frac{||\mathbf{x} _ {20} × \mathbf{x} _ {30}||}{2}\frac{\mathbf{x} _ {20} × \mathbf{x} _ {30}}{||\mathbf{x} _ {20} × \mathbf{x} _ {30}||}
+\frac{||\mathbf{x} _ {30} × \mathbf{x} _ {10}||}{2}\frac{\mathbf{x} _ {30} × \mathbf{x} _ {10}}{||\mathbf{x} _ {30} × \mathbf{x} _ {10}||})\\\\
=−\frac{\mathbf{σ}}{6} (\mathbf{x} _ {10} × \mathbf{x} _ {20} + \mathbf{x} _ {20} × \mathbf{x} _ {30} + \mathbf{x} _ {30} × \mathbf{x} _ {10})
\end{array}
$$


> &#x2753;  遗留问题， stress 如何计算？  

> &#x2705;\\(f_0\\)是\\(\sigma n\\)在绿色体截面上的积分。   
类似于上一页合力为零的原理，  
\\( \oint 截面＋\oint 表面=0\\)   
“面积／3”是因为面上的贡献均匀地分布到三个点上。  



P17     
## This stress is not that stress    

Although the use of stress tensor is the same: **mapping from the interface normal to the traction**, it can be defined by different configurations.      


|  ![](./assets/07-13.png)    |   ![](./assets/07-14.png)    |  
|----|----|
|  In FEM, we define the energy density \\(W\\) in the **reference** state.  Therefore, this stress \\(\mathbf{S}\\)  is a mapping from the normal \\(\mathbf{N}\\) to the traction \\(\mathbf{T}\\), both in the **reference** state.   | In FVM, we need \\(\mathbf{σ}\\) to convert the normal into \\(\mathbf{t}\\) for force calculation. Therefore, this stress assumes the normal \\(\mathbf{n}\\) and the traction \\(\mathbf{t}\\) are in the **deformed** state.    |  


> &#x2705;  在 reference 状态下有 normal. traction 和 stress.  
在形变状态下也有 normal traction 和 stress.    
FEM 使用的是 reference 空间下的量。    

> &#x2753; FEM是怎么用\\(\sigma \\)的？似乎只是定义了一下，没有使用。   



P18   
### Different Stresses   


We can now have different stresses, serving the same purpose but in different forms.     

![](./assets/07-15.png)   


> &#x2705;  FVM 需要的是 Cauchy Stress.（\\(\sigma \\)）、上节课讲了(S)的 计算方法，需要根据(S)求(\\(\sigma \\)).    
\\(P → \sigma \\) 的过程没有展开讲，结论在P21     



P19  
### Area Weighted Normals   

![](./assets/07-16.png)  

Now let’s figure out the relationship between \\(A^{\mathrm{ref} }\mathbf{N}\\) and \\(A\mathbf{n}\\), the two area weighted normals.    

$$
2A^{\mathrm{ref} }\mathbf{N} =\mathbf{X} _ {a0}×\mathbf{X} _ {b0}
$$

$$
\begin{array}{l} 
 2A\mathbf{n} =\mathbf{x} _ {a0}×\mathbf{x} _ {b0}=\mathbf{FX} _{a0} × \mathbf{FX} _ {b0} = (\mathbf{UDV^TX} _ {a0}) × (\mathbf{UDV^TX} _ {b0}) \\\\
\quad\quad=\mathbf{U} ((\mathbf{DV^TX} _ {a0}) × (\mathbf{DV^TX} _ {b0})) \\\\
\quad\quad=\mathbf{U} \begin{bmatrix}
  d_1d_2& \Box  & \Box \\\\
 \Box  & d_0d_2 & \Box \\\\
  \Box & \Box  &d_0d_1
\end{bmatrix} ((\mathbf{V^TX} _ {a0})×(\mathbf{V^TX} _ {b0}))\\\\
\quad\quad=\mathbf{U} \begin{bmatrix}
  d_1d_2& \Box  & \Box \\\\
 \Box  & d_0d_2 & \Box \\\\
  \Box & \Box  &d_0d_1
\end{bmatrix} \mathbf{V^T} (\mathbf{X} _ {a0} × \mathbf{X} _ {b0})\quad=d_0d_1d_2\mathbf{U} \begin{bmatrix}
  1/d_0& \Box  & \Box  \\\\
 \Box  & 1/d_1 & \Box  \\\\
  \Box & \Box  &1/d_2
\end{bmatrix} \mathbf{V^T} (\mathbf{X} _ {a0}×\mathbf{X} _ {b0}) \\\\
\quad\quad=\mathrm{det} (\mathbf{F} )\mathbf{F} ^{−\mathbf{T}}(\mathbf{X} _ {a0}×\mathbf{X} _ {b0})=\mathrm{det} (\mathbf{F} )\mathbf{F} ^{−\mathbf{T}}(2A^\mathrm{ref}\mathbf{N})
\end{array}
$$





P20   
### Different Stresses    

Now we know: \\(A\mathbf{n} =\mathrm{det} (\mathbf{F})\mathbf{F^{−T}} (A^{\mathrm{ref}}\mathbf{N} )\\).     


We also know the force can be calculated using two different stresses:    

$$
\mathbf{f} =−\frac{1}{3}  {\textstyle \sum {A^{\mathrm{ref} }}}\mathbf{PN} =−\frac{1}{3}\sum A\mathbf{σn} 
$$

Therefore, we get:

$$
\mathbf{P} (A^{\mathrm{ref} }\mathbf{N} )=\mathbf{σ} \mathrm{det} (\mathbf{F} )\mathbf{F^{−T}} (A^{\mathrm{ref} }\mathbf{N} )
$$

$$
\mathrm{det} ^{−1}(\mathbf{F} )\mathbf{PF^T=σ} 
$$




P21  
### Different Stresses

We can now have different stresses, serving the same purpose but in different forms.     


![](./assets/07-17.png)  




P22 
### The Finite Volume Method   

The previous analysis suggests we can use reference normals instead.     


![](./assets/07-18.png)  

Second Piola–Kirchhoff stress:    
\\(\mathbf{S} =\frac{∂W}{∂\mathbf{G}}\\), as in previous FEM formulation    


> &#x2705; 第一行公式：用 deformed position 计算 deformed position. 第二行公式：用 ref position 计算 deformed position, 因此直接把\\(\sigma \\)换成 \\(\mathbf{P} \\) 就可以。   
好处：ref position 是常数，可以做预计算、并存储为\\(b_1\\).   
F：deformation gradient.见P5     
公式用三用不同定义的 stress 来算力、目的是得到计­算最友好的公式    
此处内容涉及材料力学、    



P23   
### The Finite Volume Method   


![](./assets/07-19-01.png)  



> &#x2753;  \\(\mathbf{X}_ {20}^\mathbf{T} b_1\\)的计算公式中、绿色的\\(\mathbf{X}_ {01}×\mathbf{X} _ {21}\\)怎么变成了\\(\mathbf{X}_ {20}\times \mathbf{X}_ {10}\\)？下面的\\(\mathbf{X}_ {30}^\mathbf{T} b_1\\),也一样。   

> &#x2705;因为\\(\mathbf{X}_o，\mathbf{X}_1，\mathbf{X}_2\\)是同一个三角形上的顶点，任意两条边做cross都是一样的，处理好正负就好了。   
也可以用cross的乘法分配律得出相同的结论    



P24   
### Therefore,   

We get:

$$
\begin{bmatrix}
 \mathbf{X} _{10} & \mathbf{X} _{20} &\mathbf{X} _{30}
\end{bmatrix}^\mathbf{T} \mathbf{b} _1=\begin{bmatrix}
 \mathbf{X} _{10} & \mathbf{X} _{20} &\mathbf{X} _{30}
\end{bmatrix}^\mathbf{T}(\mathbf{X} _{01}×\mathbf{X} _{21}+\mathbf{X} _{21}×\mathbf{X} _{31}+\mathbf{X} _{31}×\mathbf{X} _{01})=\begin{bmatrix}
 6Vol\\\\
 0\\\\
0
\end{bmatrix}
$$

$$
\begin{bmatrix}
 \mathbf{X} _{10} & \mathbf{X} _{20} &\mathbf{X} _{30}
\end{bmatrix}^\mathbf{T} \mathbf{b} _2=\begin{bmatrix}
 0\\\\
 6Vol\\\\
0
\end{bmatrix}
$$

$$
\begin{bmatrix}
 \mathbf{X} _{10} & \mathbf{X} _{20} &\mathbf{X} _{30}
\end{bmatrix}^\mathbf{T} \mathbf{b} _3=\begin{bmatrix}
 0\\\\
 0\\\\
6Vol
\end{bmatrix}
$$


$$
\begin{bmatrix}
 \mathbf{b} _{1} & \mathbf{b} _{2} &\mathbf{b} _{3}
\end{bmatrix}^\mathbf{T} =6Vol\begin{bmatrix}
 \mathbf{X} _{10} & \mathbf{X} _{20} &\mathbf{X} _{30}
\end{bmatrix}^{-\mathbf{T}}\\\\
\quad\quad=\frac{1}{\mathrm{det}( \begin{bmatrix}
 \mathbf{X} _{10} & \mathbf{X} _{20} &\mathbf{X} _{30}
\end{bmatrix}^{-1})} \begin{bmatrix}
 \mathbf{X} _{10} & \mathbf{X} _{20} &\mathbf{X} _{30}
\end{bmatrix}^{-\mathbf{T}}
$$




P25   
## A Quick Summary    

![](./assets/07-20.png)  


P26   
## After-Class Reading   

重点推荐：   
Teran et al. 2003. *Finite Volume Methods for the
Simulation of Skeleton Muscles*. SCA.     


> &#x2705; 这篇论文重点推荐，但论文中的公式与 PPT 中的不完全一样. PPT 上的又进一步简化。    



P27   
## After-Class Reading (Optional)   


Volino et al. 2009. *A Simple Approach to Nonlinear Tensile
Stiffness for Accurate Cloth Simulation*. TOG.    

> &#x2705;2D有限元   


P28   
# Hyperelastic Models   


> &#x2705; 前面的内容，都假设使用 StVK 材料、优点是简单；缺点是无法处理反转。因此在材料力学中不常用。  
Hyperplasia 利用能量密度(W)、提供一个从 Strain (G) 到 Stress (S)的映射   
 



P29   
## First Piola–Kirchhoff stress    

We treat the first Piola–Kirchhoff stress tensor \\(\mathbf{P}\\) as a function of deformation gradient \\(\mathbf{F}\\):     

$$
\mathbf{f} _0= −\frac{\mathbf{P} (\mathbf{F} )}{6}(\mathbf{X} _{10}×\mathbf{X} _{20}+\mathbf{X} _{20}×\mathbf{X} _{30}+\mathbf{X} _{30}×\mathbf{X} _{10})
$$

It converts an interface normal \\(\mathbf{N}\\) in the reference state to a traction \\(\mathbf{t}\\) in the deformed state. 

$$
\mathbf{t}=\mathbf{P} (\mathbf{UDV^T} )\mathbf{N} 
$$

![](./assets/07-21.png)  


> &#x2705;   没讲，



P30  
## Rotation-Invariance    

The stress tensor \\(\mathbf{P}\\) is rotation-invariant to \\(\mathbf{U}\\):    

![](./assets/07-22.png)  


$$
\mathbf{P} (\mathbf{UDV^T} )=\mathbf{UP} (\mathbf{DV^T} )
$$


> &#x2705;   没讲，


P31  
## Isotropic Materials     

The stress tensor \\(\mathbf{P}\\) is rotation-invariant to \\(\mathbf{U}\\):    

![](./assets/07-23.png)  

$$
\mathbf{P} (\mathbf{DV^T} )=\mathbf{P} \mathbf{(D)V^T} 
$$


P32   
### Isotropic Materials    

![](./assets/07-24.png)   

In many literatures, people parameterize \\(\mathbf{P} (I_\mathbf{C},II_\mathbf{C},III_\mathbf{C} )\\) by principal invariants, for:    

$$
I_\mathbf{C} =\mathrm{trace} (\mathbf{C} )=λ_0^2+λ_1^2+λ_2^2
$$

$$
III_\mathbf{C} =\mathrm{det} (\mathbf{C} ^2)=λ_0^4+λ_1^4+λ_2^4
$$

$$
II_\mathbf{C} =\frac{1}{2} (\mathrm{trace} ^2(\mathbf{C} )−\mathrm{trace} (\mathbf{C} ^2))=λ_0^2λ_1^2+λ_0^2λ_2^2+λ_1^2λ_2^2
$$

\\(\mathbf{C=U^TU}\\) is the right Cauchy-Green deformation tensor.    

> &#x2705; 符号解释：\\(\mathbf{P}\\)：First… Stress、 \\(\mathbf{F}\\)：Deformation Gradient、各向同性公式认为：\\(\mathbf{P}\\) 是关于 \\(\mathbf{F}\\) 的函数、对F做 \\(\mathbf{SVD}\\) 分解可得到 \\(\mathbf{UDV^T}\\)，其中\\(D\\)是对角矩阵、其对角元素描述了三个方向的拉伸的量、把公式中的旋转分量剔除掉、 \\(\mathbf{P}\\) 只与 Principal stretches 有关。    
\\(Ic、 IIc. IIIc\\) 的定义是基于材料学、数学的先验知识     



P33   
### Isotropic Models    

![](./assets/07-25.png)   


> &#x2705; 材料力学中更常用 neo-Hookean    

> &#x2705;Fung常用来模拟人体组织。  



P34   
### Isotropic Materials   


Anyway, we still use the principal stretches for computation:   

$$
\mathbf{P} (λ_0,λ_1,λ_2)=\begin{bmatrix}
 \frac{∂W}{∂λ_0}  & \Box  &\Box  \\\\
 \Box  & \frac{∂W}{∂λ_1}  & \Box \\\\
 \Box  & \Box  &\frac{∂W}{∂λ_2} 
\end{bmatrix}
$$


And we compute the first Piola-Kirchhoff stress as:   

$$
\mathbf{P} = \mathbf{UP} (λ_0,λ_1,λ_2)\mathbf{V} ^\mathbf{T} 
$$


P35   
## A Quick Summary (cont.)   

![](./assets/07-26.png)   




P36    
## The Limitation of StVK    

![](./assets/07-27.png)   

Irving et al. 2004. *Invertible Finite Elements For Robust Simulation of Large Deformation*. SCA    


> &#x2705; 纵轴是力、横轴长度为弹簧长度、参考长度是1， 因此横轴为1时纵轴为0. 横轴 > 1 代表拉伸、拉伸越大代表力越大。但压缩时， \\(StVK\\) 表现出的力不对，且当弹簧（四面体）反转以后，力也会反转，这种表现也不对，因为最后会停在横轴-1的状态上。    



P37  

![](./assets/07-28.png)   


> &#x2705; Poison Effect： 弹性体往上拉时两边会凹进去，本质原因是保体积。   

P39   
# A Summary For the Day    


 - FEM uses the **derivates** of the strain energy function to obtain the force.    

 - FVM uses the **integral** of the interface traction to obtain the force.    

 - The two approaches lead to the **identical outcome**, in **different formulations**   

 - Hyperelastic models define the strain energy function by principal stretches, i.e., the singular values of the deformation gradient.    

- For isotropic materials, we can calculate the stress through diagonalization.   


> &#x2705; Level：1. 了解，会用；2. 理解、举一反三；3. 跳出图形学；   
图形学关注的不是数学模型，而是快。   


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/