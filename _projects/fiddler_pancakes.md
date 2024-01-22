---
layout: page
title: Fiddler_pancakes
description:
img: 
importance: 2
category: work
---
[Fiddler Problem: Can You Make It Home in Time for Pancakes?](https://thefiddler.substack.com/p/can-you-make-it-home-in-time-for)  
The four siblings can meet several times all 4 again during their walk. Wlog we assume they never meet again all four.(see Discussion at the ending)
Denote the total length L and the players A,B,C,D with speeds L/10,L/20,L/30,L/60. Player A picks a person.(1st pick) For optimization purpose, 
A will drop before home whoever she picked, so that she can go back and the dropped person can meanwhile reach the home. Player A goes back and picks another one.  
(2nd pick). Now A returns and we argue she has to drop 2nd pick to 1st pick. Because if she drops before reaching the 1st, it is not an ideal solution-
she could have dropped the 1st earlier. After this, A goes back second time and picks the 3rd. Ideally, she reaches the home at the same time with 1st and 2nd.    
So we can split the events into several parts:   
1) A drops 1st, goes back to the other two  (time 1)  
2) picks 2nd, goes back to 1st (time 2)  
3) goes back to the last  (time 3)  
4) they all rush to home (time 4)  
This way we create several segments of the trip:    
{% raw %}Start---|---|---|---|---End {% endraw %}, and denote the lengths of these segments: $$t,u,x,y,z$$.    
Case 1) Suppose 1st is B, 2nd is D, 3rd is C.  
Then during the time C walks $$t$$, then A walks $$t+2u+2x$$ (she returns). So we have the equation:
$$
\begin{equation}
30t/L=10/L(t+2u+2x) \mbox{time 1}
\end{equation}
$$
Similarly, we obatin the following equations:
$$
\begin{equation}
20t/L=10/L(u+x+y) \mbox{time 2}
30t/L=10/L(u+2x+2y) \mbox{time 2+time 3}  
20t/L=10/L(2x+2y+z) \mbox{time 3+time 4}
t+u+x+y+z=L
\end{equation}
$$
Note that total time is $$T=$$ time 1+time 2+time 3+ time 4$$=10/L(t+3u+5x+3y+z)=10/L(L+2u+4x+2y)$$  
Solving the above system of equations we obtain $$T=$$.  
If we have other cases, not that only the right hand terms change, which are the one corresponding to: max(2nd,3rd) (equation1), 1st (equation2), 3rd (equation 3), max(1st,2nd) (equation 4). For case 1) these were (3,2,3,2)*10.  
Case 2) (1st,2nd,3rd)=(B,C,D). This case is clearly slower than the first.  I calculated though $$T=$$.
Case 3) (1st,2nd,3rd)=(C,B,D). Coefficients (2,3,6,2). Here, $$T=$$


