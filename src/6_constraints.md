P2   

# Topics for the Day

 - Strain Limiting and Position Based Dynamics    
 - Projective Dynamics   
 - Constrained Dynamics   

P4  
# The Stiffness Issue    

 - Real-world fabrics resist strongly to stretching, once they stretch beyond certain limits.   
 
 - But, increasing the stiffness can cause problems.  
     - Explicit integrators will be *unstable*    
       - Solution: smaller time steps and more **computational time**.    
     - The linear systems involved in Implicit integrators will be *ill-conditioned*.     
       - Solution: more iterations and **computational time**.   
 - Can we achieve high stiffness, with a low computational cost?    


> &#x2705; 当弹簧系数大的情况下，仍能保证系统稳定。   


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/