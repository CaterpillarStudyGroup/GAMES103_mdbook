
# Implicit Imcompressible     


```mermaid
flowchart LR
    A[当前状态] -->|预测步| B[中间状态]
    B --> E[未知量：位置修正] 
    B --> F[预测位置] 
    B --> G[预测密度]
    B --> H[期望密度]
    E & F --> I[基于动量的公式①]
    G & H --> J[基于密度约束势能的公式②]
    I & J --> K[构建方程组]--> L[解出$$\Delta x$$]--> M[下一时刻状态] --> A[当前状态]
    
```


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/

