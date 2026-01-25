# Two Types of Simulation Approaches  

数值模拟方法可分为拉格朗日方法和欧拉方法两大类。

|Lagrangian Approach|Eulerian Approach|
|---|----|
|  ![](../assets/10-1.png)   |  ![](../assets/10-2.png)  |  
| &#x2705; 无 Grid. 物理量附加在粒子上，粒子运动时更新自身物理量。 | &#x2705; 固定 Grid. 物理量固定在 Grid 上。粒子运动后统一新格子的物理量。   |
|拉格朗日法中计算网格随物质一起变形，可方便地跟踪材料界面和引入与变形历史相关的材料模型，但对于涉及特大变形的问题会因网格严重畸变而产生数值求解困难，且难以有效地模拟材料的破碎、融化和汽化等行为。此类方法代表性程序为DYAN。|欧拉法中计算网格固定在空间中，不存网格畸变问题，但不易跟踪材料界面，且非线性对流项也会导致数值求解困难。|

# 粒子法与网格法的结合

### Motivation
 
- **Recall that a fluid solver usually has two components**:
  - **<u>Advection</u>** (evolving the fields)
  - **<u>Projection</u>** (enforcing incompressibility)
- **Eulerian grids are really good at projection**:
  - Easy to discretize
  - Efficient neighbor look-up
  - Easy to precondition (geometric multigrid)
- **But Eulerian grids are bad at advection...**
  - Dissipative: loss of energy and geometry


## 常见方法

![](../assets/10-2-1.png) 

## **发展趋势**
1. **多尺度耦合**：如量子-分子动力学-连续体的跨尺度模拟。
2. **机器学习加速**：用神经网络替代部分网格求解或粒子交互。
3. **高性能计算优化**：针对GPU/异构计算设计混合算法。

# Reference

|ID|Year|Name|解决了什么痛点|主要贡献是什么|Tags|Link|
|---|---|---|---|---|---|---|
||2005|Animating sand as a fluid|将FLIP方法应用于不可压缩流模拟。这使混合流体模拟达到了新的高度，得以以更高的精度和稳定性探索复杂的流体动力学。|
||1999|Stable fluids|该方法最终使得稳定的、三维的、基于物理的流体仿真成为可实现的目标，并能生成逼真的流体效果。这是首个无条件稳定的流体仿真方法，引入了半拉格朗日平流的概念，也是该领域最早应用混合仿真思路的研究之一。   ||里程碑|
||1986|FLIP: A method for adaptively zoned, particle-in-cell calculations of fluid flows in two dimensions. Journal of Computational Physics Vol|**流体隐式粒子法**|
||1962|The particle-in-cell method for numerical solution of problems in fluid dynamics.|**质点网格法**|


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/