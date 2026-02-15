# 非线性方程求解转化为优化问题

求解的非线性方程如下，其中\\({x} ^{[1]}\\)是未知量。  
$$
\mathbf{x} ^{[1]}=\mathbf{x}^{[0]}+∆t\mathbf{v} ^{[0]}+∆t^2\mathbf{M} ^{−1}\mathbf{f} (\mathbf{x}^{[1]})
$$

P14   

$$
\mathbf{||x||_M^2=x^TMx} 
$$

> &#x2705; Note that this is applicable to every system, not just a mass-spring system.    


把公式处理一下得，  
$$
x^{[0]}+Δtv^{[0]}+Δt^2M^{-1}f(x^{[1]})-x^{[1]}=0
$$
左右两边同时乘以\\(\frac{M}{Δt^2}\\)得   
$$
\frac{1}{Δt^2} M(x^{[1]}-x^{[0]}-Δtv^{[0]})-f(x^{[1]})=0
$$  
这里面唯一的未知量是\\(x^{[1]}\\)，定义函数
$$
y=\frac{1}{Δt^2} M(x-x^{[0]}-Δtv^{[0]})-f(x)
$$    
当\\(x = x^{[1]}\\) 时，\\(y = 0\\), 即 \\(y(x^{[1]}) = 0\\)   
从另一个角度讲， 
$$
\begin{eqnarray}
x^{[1]} & =  \mathrm{argmin}& F(x)\Rightarrow {F}' (x^{[1]}) & = & 0
\end{eqnarray}
$$   
因此, \\({F}' (x) = y. \quad F(x) = \int ydx \\)       
反之则不一定成立，\\({F}' (x) = 0\\) 解出的 \\(x\\) 有可能是极大值点，所以还要看 \\({F}' (x)\\) 的正负。



---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/