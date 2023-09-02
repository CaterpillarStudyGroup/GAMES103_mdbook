P47   
# A Summary For the Day   

 - Collision handling involves two steps: *collision detection* and *collision response*.    
 
 - Collision detection contains two phases: *broad-phase culling* and *narrow-phase test*.    
 
 - There are two types of collision detection tests: *discrete* and *continuous*.    
 
 - Similarly, there are discrete and continuous collision responses.   
 
 - For continuous collision responses, we must update the state to become collisionfree state. There are two approaches: *interior point method* and *impact zone optimization*. **Rigid impact zone is also a method, but it’s problematic**.    

 - For discrete collision responses, we allow intersections to stay and hope to remove them in long turn. **Cloth-cloth intersections are difficult to handle**.    


> &#x2705; 如果考虑摩擦，通常把摩擦做为后处理，但这样结果不精确。如果同时处理摩擦和碰撞、会很复杂。   
> &#x2705;Impulse方法的碰撞检测通常用SDF．但很多形变体无法使用SDF.    
> &#x2705;Impulse响应方式是离散响应方式，无法处理穿透问题。   
> &#x2705;碰撞问题通常不使用物理方法，因为使用物理方法需要小步长，效率非常低。  
> &#x2705;碰撞开源代码：bullet. physics X   


---------------------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES103_mdbook/