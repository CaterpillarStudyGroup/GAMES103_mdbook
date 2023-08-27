P37  
# A Summary For the Day    

 - Position-based dynamics and strain limiting    
    - The key is to build a projection function for every constraint.    
    - Two approaches for integration: Jacobi and Gauss-Seidel.   
    - Fast in low resolutions, but problematic in high resolutions.    
    - Not physically correct.    
 - Projective Dynamics    
    - Also uses projection functions, but they are now built into energies.    
    - In every iteration, projections are first updated, and then treated as constants in implicit formulation.    
    - The matrix in the system becomes constant, can be pre-factorized for fast simulation.    
    - Converges fast only in the first few iterations, slow afterwards. CPU friendly.    
 - Constrained Dynamics   
    - Focused on very stiff constraints. Introduces dual variables.    
    - Also built upon implicit integration. Two methods: primal-dual, pure dual.    
    - Restrictions on the solvers.    



---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/