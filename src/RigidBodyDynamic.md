Lecture 03
Rigid Body Dynamics [59州 的
Rigid Body。刚体，物事体表面不会发生形变
Simulator。更新刚体在某时絩的状态 St
reference。参照状态 -.­-状态：旋转 R.平移 T.缩发-
#平移运动㫁
为： flxltl.vcti.tl
继体受到的12 可能跟.tt? 置速度.时间都有关
㽉涧= vct.lt 凹么！国 dt
质量
位置
ME)二七(to) tffvc.tl dt
##求积分 [1：11：11]
有限区间的积分=求积分区间的面积
1段设要求 lǎfmdx,此处有三种方法，
0 Explicit Euler
lǜtm 收~~ fun.(b-a)

② Implicit Euler
约以1 dx~flbi.ch-a) 16
③ Mid-point
临从1比吼幽。(b-a)
##平移运动中的积分解法
公式1用 Exploit,即 因质量，有䵼蠶示
vctn-vlt.it 心-M"-f （我。）
公式2用 Implicit、即
Mtv) = xwitot.vl.tn)
此方法称为 leapfrog [1：21：19]
##力
重力： Gravity Force, f = Mg
阻力： Drag Force, f =-o v
或简化方法.li 20
It#平移运动相关的状态更新
l. 分别计算每个刀
䀞鸁卜目
4-更新5.name
Simulators
-

Ft 能转运动
##旋转的表示方法. 17
-旋转矩随
优蕊 义二 RN、使用方便
敬琏0有冗余，用9个元齦示3个自由度
② 不直观
③ 雦求导1计算角速度）
。区人拉角：
☆ 适用场景。 design. control
优点直观
局限性.10万向节死锁(gìmbd look)，出难以求导
国无米玫 比32：40]
q =[5. 0]
实䴊防高虚收部分，是向是 i.j.la.
g = [as, a v]
q ± q = [8 IS-. 0.±$以]
q x q =[sina.U28N.tsw.tr.mg
11911： Fit
用四元数表示方叇转[1：39：子0了
G. /'ˇ q =[cos I U]
且满是 11911=1

优点
l. 直观
2可以方便地转成欧拉角和矩阵 18
# tt 旋转运动与时间的关系
torque:力矩， inertia:惯性的]
[1：45246]
r i = Rri: 点 ri 经过旋转矩阵贬后的位置
Ii = r'： X fi.点 ri 受到为 fi 后的为琏力矩
[=[Ii : object 受到的总的力矩
Irg =[milririi-r.ir il
I 二 RI ret R' q、对应质量咋对酬'
{W （1） = W （0） t 心（20105'九回 龘
qa)= W) t [oitwythqc.co)
I
此公式对照比15）的公式一起看， 醚𡤅
建议每一步之后都对9做 Normalize
## 旋转运动相关的状态更新
o q → B
㦔靈𪆫䯀，
⑤ 更薪 w 讲 Unity 的部分跳过了

选读材料。
[1：51：46了 19
https://gnaphics-pixan.com/pbmzool
Rigid Body Dynamics
#补充。
011210[Iterative Linear Solver]
如果取 Me A,一步即可完成迭代
② 本节课都用局部坐标系
lecture 04补充
tt Torque 力矩 [12-55了
一种会导致物体旋转的力
titti-l.in
Torque 是由力导致的高锻，用 E 表示，
正的方向： tfi.IR ri
Ti 的大小。与 fi 成正比， 与 Rri 成正比
与 since 成更比， 0为 Rri 与小的无角
井 Inertia 转动惯量
理解为对方链专趋势的抵术儿.
Iron 与旋转轴的方向有关，因此是一个矩阵
当兔子的姿势改变时， hen 地会改变，因此与㕷关


