# Lecture 02

# 数学基础：  Vector, Matrix, Tear Calculus

# Vector 

矢量：黑体，小写 标量：斜体 矩阵：黑体，大写

右手坐标系：OpenGL， Research

左手坐标系；Unity，Dired-X [06：34图]（假设物体都在屏幕后面）

Vector 有时只是被用于一堆数据的集合，维度不一定是物理上有意义的维度。

GAMES 101讲过的，不重复

Vetor 的加减法使用场景

l.描述线性公式[16:51]

2.线性差值[17：51]

3.描述 line, ray, segment

Norm 范数 [link] ()

Vector 的 Norm 使用场景:

1. 距离 →只关心大小，不关心方向

2. 单位向量 →只关心方向，不关心大小

3. 向量单位化 →只关心方向，不关心大小

点乘

p·q ，< p,q > , $p^Tq$ 表达点乘的不同（写法）

应用

1.点到线的映射[29:42]

2.判定点和平面的半凉[35：40]

8=<p-c, n> {20，在平一 above
=0， on
个 so, below
signed distance to the place
3、 Panned 一 Sphere 碰䡴栓测[40240]
1112心-412= r-
器材 tv
⇒ 一无二次方程 {1比比比： 不碰撞
one. not,轨迹相切
two. not。穿过， It..ly 的
碰撞

熙计算三角形的面积和法向量比853] 6
ⓝ = X 10二人一 Xo to 二人 to
h. = 以104×心 .name
此心 XX。用
A: Mwllhk 妆。此。11/2
Not。几的方向与顶点的顺序有关
212在三用形的内或外
详见6AMtsy-nnsththotstosnnshr.­in.重心坐标， Baryonic Grandes。[1人0556了
Ayy 利用公式计算从淼红的
※ 面积1豳 Aa)。
A = Not At A、
P 的重心坐标为
深，獘，影。
通常用于插盒[1人0飞39了

Etrahednalvolu.me 四面体一，
T.li 12：50] 1. signed volume 7
v = j h. A
=扎㤈焱器慥灿。比11）
= È Not. XX.）
州个个个个1 比4行列式
体积是 Signed Volume.[146：30了
2[l'-18-18] Baryonic Weights
类似于三角形
1. particle、 triangle 碰控检叫[1：21：20]
（12(tl-Xoj-Xoxx.no 二 0
t = CR-xol.to/lxzo-­v.XoXXzo­t 为与三角形所在平面相交的时刻，
还需检查吣是否在三角形内
tt 矩阵 Men 比25：4门 、， if ii 单血
嚼着 fǎfnǎg 0㗊以森正 aiaj-fo.fi#j 正交

A' A = I ⇒ A:心
来312正交矩阵可作为正交矩阵 8
2 造鞋直分解。 Singular Value Decomposition
A = U DU
正交矩 正舜 一正交矩阵
对角矩阵，
对甩线上的元素为奇部真
理解 [1241：40]☆☆☆
口 i D 孽㽊纞 D
能有的 A 都能8以
3.特征值分解 Eigen value Decomposition
, A = U 12 W
r
必须是对称矩阵 特征值的对用矩阵
来作为 s v 口的特殊情况
4. 非对称矩阵的特征但分解
这种情况下特征值为虚数
返 CG 中不考虑这种 case
5. 对称正定 sg-gmme.tn Positive Definiteness
cs.p.ch
[1：51：00]

定义，一
对任意 v.li to,满足. g­ot A v 20 ⇒ A 区定
0「A v e o ⇒ A 半正定
理解。
A 正实如所有特征值为𥺼
檲 A 䶲捅占优
用于有限元
A 正定⇒13-[朵 À]半起定
#线性系统 Line solver
Ax = b .已知 A. b,求 X
1.先求 心， 人 A" b
A 很大⇒计算 A"耗时.
A 稀疏但心不稀疏⇒更多存储空间
2 Direct Linear Solver.
A = LU­Axz.LU x = b.
Step 1： 能 Ly 二 b
Step 2. 解 Ux = y
O 通常在 Sept 之前加一步 permutation,保证人和4健
尽董稀疏
0如果 A 不变，山分解只需估心先
建

Lecture 03
Rigid Body Dynamics 比
接上节课 s-p.cl
3-难以并行化计算
长井 Iterative Linear Solver
廵=心+2 M"(b-A i)
M. 整代么？要求 M'容易计等 一声
① 对角矩阵，取 A 的对角元素。 Nkdòg 间
Jacobi 方法'
② Gauss-Seidel 方法，
Me lower (A)
40 More_
收敛条件。
f (I-2 AM"14
辆矩阵的最大的特征值 、
綖特点10实现容易02高效但不精确
③ 可并行计算
局限性，.0有收敛条件20难以得到精确解

# tensor Calculus [30252]
# t.lt-order Derivatives
###HER. 11
g =毒 dxt 凤青 g +聂兆 Noei 和人不同
=[聂等剟潉] T =比以2）ㄒ
⇒ 聂=淡等剟
或灈䥹 ，...
井井井旭）=[籥！ À 种不同，
拟）=盛/聂等是 心和人不同
聂等瓷
灵哥 叕/ tin 矩阵
相关概念。 Divergence
区。非聂士等七器 相当于矩阵的 trace
axì =[翡器，是一叕毙载在一签越中见过类的
写法

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

