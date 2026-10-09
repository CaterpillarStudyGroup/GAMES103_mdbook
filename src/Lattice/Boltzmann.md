# 动理学基础

## **两种描述层级**

[流体力学](../Physics/Fluid.md) 中的欧拉网格法求解的是**宏观量**：密度 \\(\rho(\mathbf{x},t)\\) 与速度 \\(\mathbf{u}(\mathbf{x},t)\\)，方程是 Navier-Stokes 方程。

动理学（kinetic theory）换一个层级，用**速度分布函数**描述流体：

\\[f(\mathbf{x}, \boldsymbol{\xi}, t)\\]

它的含义是：在时刻 \\(t\\)、位置 \\(\mathbf{x}\\) 附近单位体积内，速度落在 \\(\boldsymbol{\xi}\\) 附近单位速度区间内的分子数。

这是连续介质假设**下面的一层**：连续统里的流体微团，在这里被看成大量分子的统计集合。

## **从分布函数提取宏观量**

宏观量是分布函数的**矩**：

\\[\rho = \int f \, d\boldsymbol{\xi}, \qquad \rho\mathbf{u} = \int \boldsymbol{\xi} f \, d\boldsymbol{\xi}\\]

二阶矩给出动量通量张量：

\\[\boldsymbol{\Pi} = \int \boldsymbol{\xi}\boldsymbol{\xi} f \, d\boldsymbol{\xi} = \rho\mathbf{u}\mathbf{u} + p\mathbf{I} - \boldsymbol{\sigma}\\]

其中 \\(p\\) 是压强，\\(\boldsymbol{\sigma}\\) 是粘性应力张量。这一步说明：**只要知道 \\(f\\)，Navier-Stokes 方程里的所有宏观量都能算出来。**

## **玻尔兹曼输运方程**

\\(f\\) 的演化由玻尔兹曼输运方程给出：

\\[\frac{\partial f}{\partial t} + \boldsymbol{\xi}\cdot\nabla_{\mathbf{x}} f = \Omega(f)\\]

- 左端：分子在无碰撞情况下的自由飞行，即**迁移**
- 右端：\\(\Omega(f)\\) 是**碰撞算子**，描述分子间碰撞引起的分布变化

这个方程的两项与后面格子气自动机的两个步骤完全对应。

### 碰撞算子的性质

碰撞不产生也不消灭质量与动量，所以

\\[\int \Omega(f) \, d\boldsymbol{\xi} = 0, \qquad \int \boldsymbol{\xi}\, \Omega(f) \, d\boldsymbol{\xi} = 0\\]

对玻尔兹曼方程两端关于 \\(\boldsymbol{\xi}\\) 取矩，就得到宏观的连续性方程与动量方程。这是"从动理学还原到连续统"的第一层含义。

### 平衡态

碰撞使分布趋于局部平衡。令 \\(\Omega(f)=0\\) 得到的解是 **Maxwell-Boltzmann 分布**

\\[f^{eq} = \frac{\rho}{(2\pi R T)^{D/2}} \exp\left(-\frac{|\boldsymbol{\xi}-\mathbf{u}|^2}{2RT}\right)\\]

H 定理保证这个平衡态是碰撞的吸引子，也就是熵最大的状态。

## **BGK 近似**

完整的碰撞算子是复杂的积分，工程上常用 **BGK 近似**（Bhatnagar-Gross-Krook, 1954）：

\\[\Omega(f) \approx -\frac{1}{\tau}\left(f - f^{eq}\right)\\]

物理含义：分布 \\(f\\) 以时间常数 \\(\tau\\) 松弛到局部平衡分布 \\(f^{eq}\\)。

- \\(\tau\\) 大 → 松弛慢 → 粘性大
- \\(\tau\\) 小 → 松弛快 → 粘性小

这个近似把碰撞从一个积分算子简化成一次代数插值，是 LBM 能高效实现的关键。从形式上看，它也是 LBM 里唯一带参数的环节。

## **从动理学还原到 Navier-Stokes**

把 \\(f\\) 按一个小参数 \\(\epsilon\\)（与克努森数同量级）展开：

\\[f = f^{(0)} + \epsilon f^{(1)} + \epsilon^2 f^{(2)} + \cdots\\]

代入玻尔兹曼方程并按 \\(\epsilon\\) 的阶次分离，这一过程称为 **Chapman-Enskog 展开**：

|阶次|内容|结果|
|---|---|---|
|零阶|\\(f^{(0)} = f^{eq}\\)|给出 \\(\rho\\) 与 \\(\mathbf{u}\\) 的定义，对应无粘的欧拉方程|
|一阶|\\(f^{(1)}\\) 由迁移项驱动|给出粘性应力张量|
|二阶|闭合|还原出完整的 Navier-Stokes 方程|

这是动理学方法的理论保证：**玻尔兹曼方程在宏观极限下就是 Navier-Stokes 方程。** 后面 LBM 的粘度公式也是从这一步得到的。

## **三层描述的关系**

|层级|描述变量|演化方程|离散化后得到|
|---|---|---|---|
|连续统（宏观）|\\(\rho, \mathbf{u}\\)|Navier-Stokes|有限差分 / 有限体积 / 有限元 + 投影法|
|动理学（介观）|\\(f(\mathbf{x},\boldsymbol{\xi},t)\\)|玻尔兹曼输运方程 + BGK|**格子玻尔兹曼方法 LBM**|
|分子（微观）|每个分子的位置与速度|牛顿第二定律|分子动力学 MD|

本章要讲的 LBM 位于中间层：它比宏观方程多保留一个速度维度的信息，因此不需要额外解压强泊松方程；又比微观分子模拟粗得多，因此计算量可控。

---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/
