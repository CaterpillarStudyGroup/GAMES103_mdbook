# GAMES 103

# 基于物理的计算机动画入门 

# Lecture 01

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

简单，通常是 raw da from scan,不能直接用于渲染

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

goa.lt:
计算 object 在每个 time step 的状态，汰态由具体应用

而定，可以是：

p.0， p, 外观..…

Note time step 可以与帧率不一至文

根据 object 特点分类。

刚体 igit body,， Mesh,粒子（模拟刚体破碎了 3

and Hair, Nh mesh

弹性物体：姚 body.

流体液体气体|糊(re。以测，体素、烟，

水、 Meh, 做。

（实时）
（小花 粉，体素
Mesh 用 face 把所有心比连成一个整做.适用于飘
性要疑强的对家.
Particle 把每个比比当作一个独立的个体，每个个体对自己
的运动负责适用于松散的对家
Grid 行相者之间，把 object 划分成 gmd.gg 但 grid
之间又存在连续性。

