Lecture 04
Rigid Body Contacts .
It 粒子(Particle)的碰撞检测与响应[35：00]
' ## 812 F (Signed Distance Function)
8日 Fi 0/4）。表示点倒表面 surface 的距离
符号，.点在 surface 的内或外
绝对组：距离的远近
举例：[37：18]
平面：已知平面的法向量 À 和平面上的一点 p.
44） = (x-p)。几
球面：已知球面的圆心和丰经 r
中以7=1比41-r
图上公式的不应该为斜体
柱面已无口圆柱轴的方向 n,其中一个场面的圆心12，
切面圆的半径 r.­ci rnr
盥之 lk-pi-rhh.ir
看来是作文沿国柱是无限长的
矗于
投影边 勾股定理
#Ft Surface 相交的场景（43：11）
敏 surface 分别定义中，倒籽中为%dc.ch,
若人在曲面内部，应同时满足所有中都<0.

##Surface 相并的场景[46-13]
人与任意一个曲面的碰撞都算是碰撞 𤦍
#碰撞响应
##Quadratic Penalty Method
事如果人进入到曲面内部，
就给人一个向外的力。把它推出来
为的大小 一中心 学生条件。中以10
方向。立中的
即 f =-K 4比了 N
局限性。1：
人进入曲面以后才会有力琏，
但此时碰撞(artificial)已经产生了
解决方法：
进把表面向外扩充 E。即
力的产生条件。 4比1<E
大小： 1-E-4的
方向： 在44）
f = k (e-01的） N
局限性2
K 太小，碰撞以后难以把点找出来
k 太大， 点被弹飞 (overshooting)
解决方案。(Log-Barrier Penalty Method)
k 的大小与灿有关

k-p­f.pl 中的一 N 22
引入了两个问题.
1. overshooting 仍有可能存在
这2人进入曲面后反而越走越深
井井实践中的又一
哥整两5.-.-_或设置 limit 可回避以上问题
3. 难以处理摩擦力(friction)
# Impulse Method demo
原理-当人进入曲面内部两
让人治 N 移动至曲面上。即 |更新位置
i-x.tl 中的 W
Itgrrn
更新速度。移动距离-移动方向
ⓛ 当前速度向这0。 N 30）
不须额如外处理
② 当前速度向内(U. Nco)
把0分解为 Vi 和以.
- w'=-Mr UN
- 一反弹
y'二𡦀摩擦力产生的衰减
V = W t Vi
江了什么是 Coulomb's law?.
优点.
23
L 可以控制摩擦力
2.可以控制反弹的位置
3. penny 实现简单 建樱
4刚体常用 Impulse, 衣服常用 Penalty
Fl 刚体碰撞检测[146：50]
##Naive 方法。
Xi 二 Xt Ri
正 癍比赢 ǖ 第1个班的初始位置。
第 i 个了15点
当前的缱
对每个人计算 fix)以检测碰撞
##碰撞响应
V i = U 十 W X R ri
T 是
第 i 个顶点 裢专速度方向
的速度 8赢
速度 就和 Rri
都垂直
发生碰撞时， Object 会在碰撞点受到中加.
䩍会造成的影响是，
速度的改变
V'二 Utfnj
角讉的改变.
w'= w t I'（Rrixj)

再把物体状态的改变应用到每个点上去
Vi'= v' t w x Rn i 24
想 Uitkj
完整流程汇1：37230]
##Not
l 有多个点同时发生碰撞
则。取平均 oscillation
2在物体表面振荡(resliy
試油'马小 Mi­tt shape Mt Matching
原理
1.把刚体看作是多个粒子，每个粒子独立运动
2把粒子还原成刚必
K. R}= agminzjlktRri-y.tk
优化问题，且暂时不考虑旋转矩阵811需满足的约来
① 求导并令导数为0，解海出 C
𨫎 A 求导并令导数为0：解出 A。
③ 扫一让 A 满是旋转矩阵的约束
A 二 Rs Polar Decomposition
. 。 极性种
完整流程[1汛㽊 本地形变

特总
l. 容易理解。不涉及物理 25­2容易实现
3.可以糊模拟的算法相结合
4难以保证满足约来
5-适用于对精确度要求不高的场景
拓展阅读
Mesh less Deformations Based on shape Matching,
Muller et al.2005
