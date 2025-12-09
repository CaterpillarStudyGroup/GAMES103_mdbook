# 粒子的属性

|属性|符号|在通常的仿真场景中是否可变|
|---|---|---|
|质量|m|否|
|全局位置|p或x|是|

在可变的仿真属性中，通常还会考虑它们的一阶导、二阶导等。

|属性|符号|说明|
|---|---|---|
|速度|v或\\(\mathbf{\dot{x}} \\)|p的一阶导|
|加速度|a|p的二阶导|

更新仿真对象的可变属性。   


# 粒子的仿真

当粒子同时受到多个力时，通过相加得到它们的合力。  
粒子在各种力的作用下会发生位移（transform）。其p, v, a都会发生改变。  

## 连续形式

真实的物理世界里，属性的变化是连续的。

$$
\begin{cases}
 \mathbf{v} (t^{[1]})=\mathbf{v} (t^{[0]})+ m^{−1}\int_{t^{[0]}}^{t^{[1]}} \mathbf{f} (\mathbf{x} (t), \mathbf{v} (t), t)dt\\\\
\mathbf{x} (t^{[1]})=\mathbf{x} (t^{[0]})+\int_{t^{[0]}}^{t^{[1]}} \mathbf{v} (t)dt
\end{cases}
$$

> &#x2705; 速度是加速度的积分，因此\\( \Delta v=\int a=\int \frac{F}{M} =m^{-1}\int F\\).   
> &#x2705; 位置是速度的积分，公式的本质上是解积分。   

## 离散形式

> &#x1F4A1; 为了方便计算机进行计算，需要把连续积分形式转为离散积分形式。
> 数值积分相关内容请戳这里：[link](https://caterpillarstudygroup.github.io/mathematics_basic_for_ML/NumericalAnalysis/NumericalIntegration.html)。最后结论是混合式的积分方法。

> ![](../assets/03-13-2.png)  


## 总结

![](../assets/03-14.png)    

![](../assets/03-15.png)    

> &#x2705; 质量 \\(M\\) 是一个标量

# 应用场景

粒子可以作为水分子，气体分子，烟雾分子的仿真代理。用于仿真液体、气体的效果，针对实际的应用场景，还会增加一些粒子属性。   
粒子也可以作为刚体所占用空间的代理，仿真刚体破碎的效果。    


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/