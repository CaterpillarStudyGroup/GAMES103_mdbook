# Rigid Bodies    



> &#x2705; rigid：物体很硬，因此不考虑形变。  




P7   
## Rigid Body Motion  


If a rigid body cannot deform, its motion consists of two parts: translation and rotation.   


![](./assets/03-2.png)     


> &#x2705;reference：参考状态,无平移,无旋转此时物体中心点在原点上，\\(\mathbf{x}\\) 轴向左，\\(\mathbf{y}\\) 轴向上\\(\mathbf{z}\\) 轴向前。   
当前状态：旋转为\\(\mathbf{R}\\)，平移为\\(\mathbf{T}\\). 那么物体上任意点的位置为：   
\\(\mathbf{{x}}' = \mathbf{Rx} + \mathbf{T}\\)    
刚体模拟：已知当前时刻的状态和受到的力，求下一时刻的状态。     

P6  
## Rigid Body Simulation   

The goal of simulation is to update the state variable \\(\mathbf{s} ^{[k]}\\) over time.     


![](./assets/03-1.png)     

---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/
