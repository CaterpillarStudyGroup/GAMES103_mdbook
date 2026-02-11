
# Affine PIC(APIC)    

## 背景   

PIC 的 P2G 和 G2P 过程都包含加权平均，导致速度被平均化。平均化表现为数值耗散（糊）和细节丢失（大形变时失真）。     
FLIP 算法改为传递速度增量，解决平均化问题，但引入振荡问题。    
 
## APIC 核心创新    

每个粒子维护一个额外的属性 \\(A \in R^{2\times 2}\\) 或 \\(A \in R^{3\times 3}\\), A 用于记录粒子周围的 Affine 速度场,可以描述粒子所在局部区域的速度梯度。        
    

![](../assets/10-2-99.png) 

pressure projection 一般是指解泊松方程。    

## 基本步骤   

### G2P   
 
1. 计算  \\(A_p\\)    
 
$$
A_p = \sum_I V_I \otimes \nabla N_I(x_p)
$$
 
2. 根据 \\(A_p\\) 计算 \\(v_p\\)   
 
$$
v_p = \sum_I N_I(x_p) v_I + A_p(x_p - \bar{x}_p)
$$


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/