# Introduction

# 准备工作[11：03]

1. 数学：线代，微积分

2. 编程：C，C++，C#，JS

3. 主动学习
   
# 主要内容 [17：14]

课表

# 建议

建议只读重点

建议读 paper 而不是教材

学技术而不是学 Unity

多读、多写、多想

# 图形学

几何、渲染、动画

$$ 
\text{几何}\rightarrow \text{动画}\rightarrow\text{渲染}\rightarrow \text{显示}
$$

## 几何[41：47]

—— mesh

顶点 面片（**三角形**、四边形、多边形、四面体）

要解决的问题

生成、简化、细分、优化、Volume Mesh（难点）

（在线，对后面的算法有影响）。

—— 点云 

简单，通常是 raw data from scan,不能直接用于渲染

要解决的问题：

$$
\text{点云}\rightarrow \text{mesh}
$$

重采样

—— Grid 格子/体素

用于医学呈像

要解决的问题

Memory cost, volumetric 渲染（rendering) ,

## 渲染

真实渲染VS非真实渲染
 
基于 ray tracing VS 基于 rendering pipeline

材质扫描

## 动画

人体动画、物理动画 

goal:

计算 object 在每个 time step 的状态，状态由具体应用而定，可以是：

p，v，p， 外观……

Note ：time step 可以与帧率不一致

根据 object 特点分类：

刚体：right body→ Mesh, 粒子（模拟刚体破碎）

Cloth and Hair, Mesh

弹性物体：soft body，Mesh

流体，液体，气体：粒子(real-time)，体素，；水，Mesh（实时），体素；花，粒子，体素

Mesh 用 face 把所有vertex连成一个整体，适用于整体性较强的对象。

Particle 把每个vertex当作一个独立的个体，每个个体对自己的运动负责，适用于松散的对象。

Grid 介于相者之间，把 object 划分成 grid 但 grid 之间又存在连续性。


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/
