# 流体隐式粒子法（Fluid Implicit Particle, FLIP

## - **Idea: don’t gather the physical quantity. Gather the <u>delta</u> of the physical quantities before/after grid operation.**      

## 方法：      

### 网格更新    

  - grid op = pressure projection in incompressible fluid simulation    
  - grid op = internal force computation in solid simulation (MPM)   

## G2P    

PIC：\\(V_p^{t+1} = \text{gather}(V_i^{t+1})\\)     
FLIP：\\(V_p^{t+1}=V_p^t + \text{gather}(V_i^{t+1}-V_i^t)\\)，这会导致粒子速度趋于平均，表现为粒子糊掉，可液体细节消失。         
> FLIP 引入了 P2P 的信息路径来避免信息丢失。    
但纯 FLIP 会因增量传递而积累误差，所以需要少量PIC进平衡。         
FLIP0.99 = 0.99.  FLIP + 0.01PIC    
  - **PIC（流体版）**：粒子速度完全由网格插值获得，较稳定但**耗散大**。
  - **FLIP**：粒子**速度变化量**由网格插值，保留更多细节，适合高分辨率模拟。
- **应用**：计算机图形学中的流体动画（如烟雾、水）。      
 


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/