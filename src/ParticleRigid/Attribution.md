系统所假设的场景为一个粒子和一个刚体。其中粒子代表有位置无体积的仿真对向。如果系统中有多个粒子，粒子之间无相互作用，所以独立仿真每个粒子。刚体代表有位置有体积的仿真对象，换成弹性体等有位置有体积的仿真对象，此系统也适用。  
此系统主要要考虑的是刚体对粒子的作用。  

## 子系统（粒子）的属性

- 粒子属性

|属性|符号|在通常的仿真场景中是否可变|
|---|---|---|
|质量|m|否|
|全局位置|p或x|是|

- 刚体属性

|属性|符号|在通常的仿真场景中是否可变|
|---|---|---|
|质量|m（均质）或M（非均质）|否。刚体的质量为其所有粒子的质量之和。|
|全局位置（世界坐标系）|p或x|是。刚体所占的是一个连续的空间，而不是一个点。选择刚体中的某一个点（通常是质心）的位置作为刚体的位置|
|全局旋转（世界坐标系）|q <br> 旋转的表示戳这里[link](https://caterpillarstudygroup.github.io/mathematics_basic_for_ML/Geometry/Quaternion.html)。最后结论是四元数表示方法。|是|

## 组合系统（刚体）的属性

无

## 子系统聚合后产生的新属性

无

# 应用场景

实际应用场景中对单个粒子进行仿真没有意义。  
是后面多刚体仿真的基础。  