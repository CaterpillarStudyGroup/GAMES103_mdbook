# 流体隐式粒子法（Fluid Implicit Particle, FLIP
- **原理**：在流体模拟中结合粒子和网格，粒子携带速度等信息，网格用于求解压力泊松方程（实现不可压缩性）。
- **方法**：
  - **PIC（流体版）**：粒子速度完全由网格插值获得，较稳定但耗散大。
  - **FLIP**：粒子速度变化量由网格插值，保留更多细节，适合高分辨率模拟。
- **应用**：计算机图形学中的流体动画（如烟雾、水）。      
 
- **Idea: don’t gather the physical quantity. Gather the <u>delta</u> of the physical quantities before/after grid operation.**      
  - grid op = pressure projection in incompressible fluid simulation    
  - grid op = internal force computation in solid simulation (MPM)   


PIC：\\(V_p^{t+1} = \text{gather}(V_i^{t+1})\\)     
FLIP：\\(V_p^{t+1}=V_p^t + \text{gather}(V_i^{t+1}-V_i^t)\\)    
FLIP 引入了 P2P 的信息路径来避免信息丢失。    
但 FLIP too noisy，因此     
FLIP0.99 = 0.99.  FLIP + 0.01PIC    
