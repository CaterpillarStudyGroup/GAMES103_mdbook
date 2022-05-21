Lecture 05.
布料 (Cloth)物理仿真 26
#弹簧系统[5：40]
##理想弹簧 [060门
Hooks Law.
The spring force tries to restore the Ü length.
g-维.
E 以） 二 Ìk (x- 凵2
fix) =一袋=-k (x-L)
- =维 [08：00]
E 的二三'比11心州-Ù
批）=-T i E =-k 㸠州圳箭µ
fī 以1=-T)
推导过程见173
- 牧维[10228]
-结构化的弹簧关统[12-203
0 horizontal, Vertical, 构成网遑
② Diagonal, 防止余4方向的拉伸
a Bending, 阻止面料弯折

想简化版本[14246有了
一非结构化的弹簧系统 21
0每条边个弹簧.
② 增加内部边，阻止䩢
井三角形网才一具体实现方法跳过
中1集成 Ingram
tttt Explicit 湿式）
把弹宽的力结合到粒子系统中 [33：40]
0构造半屿系统。只考虑、粒子的 position.不考虑 rotation
② 在计算式的那一步增加一个弹簧力
实际计算时会先把弹黄力提前算好
局限性，
1.数值上不稳定
k 过大[36-13] （以弹簧系数） overshooting
辙决能减少比，这个方法不太好
=11#Implicit （隐式）
{心=比01 tot MY 4） a)
x.cl)= No) tot-U U) 4）
l. 公式山代入公式山，消无以1），得
24）= Not to t.no)七心心 fu)
2假8设怾与义有关，与0无关，例如動弹簧力

问题转换为解方程。
3把以上问题转换为解另一个问题 zg­xuiargmn.FM,其中
铋宼以心北北𡃈萡籯量
& M.有顶点组成的向量 lkhiimx,
质量矩阵㖷对角矩阵
非线性方程转化为优化问题
##解化化问题. Newton-Raphsm 方法
简称牛顿方法， 用手解优化问题 x.cn = arg minty
原理找到带人使得 F'比）=0.
令心为比刈的炸用域上的某一点，有
FǛT ~~ F'比4 t F"心）以心泰勤展开的
令 F'以）=0， 解出 X.得.心圵心。 二阶近似
详细步马聚：[1：01：20]
L 人随机初始化为心
之心入=_自 心（心） 一­点七些心、签 If his unni
lake
遗留问题：
l. F'比1=0处人有可能是最大组或最𡸜
解决方法：看 F"比）， F"比120⇒最大值， F"以1 to ⇒最大值

用牛顿法解当前 thin:3门
原理。 29
0=非以1 EYE 从图十一批幽灵（七灿
具体步骤。 事心人的二河 我
l. 初始化 x。 众人在时间1<下的鱼
篼'䵴…'
怎 忷<E
È Mt H 纵） 女吡的二志州兆大。一州一批1
3. Vkt = 海（灿-as YOU
优化问题 US.解线性非线性方程
以优化问题的角度理解"解线性非线性方程"的各种方法
产生的效果和问题，
# Spring Hessian 弹簧系统中的日
u:28200了 .... Hon
㤈-1！ i:1慜：：蠶
Aij 见月13.
H no-_-Am a、一二时：（比打
焽正定， 比健正定。拉伸
定？ 有可能不正实压缩 30
H 是吣的二阶导，
N)
H 正定⇒无最大鱼⇒ Fix)只有一个最小监
⇒ E'以120有唯一解
⇒ 系统璭稳定
弹簧1玉缩时， H 不一定正定
⇒ in 二0可能有多个解
⇒ 系统不稳定例子[1：38-18图了
解决方法
不正定→正定、
拓展阅读， Stable But Respire th.
Choi and ko.zooz.­tt Jacobi 方法
自的一解 A 以二 b
具体步骤：
free residual error
I 0 X-O
r = b-And
△ 仁以 ta Dy fl UP my
她比回雌断
\]一月的对电矩阵

Ft Summary [1：43：20]
Direct Solver Inane snowy
鞩.LU。旧汇 Choking
选心做 1 more
计算量 expensive 可控
精确性 exact 可控
适用场是 CPU cpuaapu
对的蠶 鞎䖩 有限制，如正定
井拓展阅读。
Large Steps in Cloth Simulation
Banff and Within.1998.
