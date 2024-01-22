--
layout: page
title: Fiddler problems
description:
img: 
importance: 2
category: work
---
[Fiddler Problem: Can You Make It Home in Time for Pancakes?](https://thefiddler.substack.com/p/can-you-make-it-home-in-time-for) 
The four siblings can meet several times all 4 again during their walk. Wlog we assume they never meet again all four.(see Discussion at the ending)
Denote the total lenght L and the players A,B,C,D with speeds L/10,L/20,L/30,L/60. Player A picks a person.(1st pick) For optimization purpose, 
A will drop before home whoever she picked, so that she can go back and the dropped person can meanwhile reach the home. Player A goes back and picks another one.
(2nd pick). Now A returns and we argue she has to drop 2nd pick to 1st pick. Because if she drops before reaching the 1st, it is not an ideal solution-
she could have dropped the 1st earlier. After this, A goes back second time and picks the 3rd. Ideally, she reaches the home at the same time with 1st and 2nd.  
So we can split the events into several parts: 
1) A drops 1st, goes back to the other two  (time 1)  
2) picks 2nd, goes back to 1st (time 2)  
3) goes back to the last  (time 3)  
4) they all rush to home (time 4)
This way we create several segments of the trip:  
{% raw %}Start---|---|---|---|---End { endraw %}, and denote the lengths of these segments: $$t,u,x,y,z$$.
Case 1) Suppose 1st is B, 2nd is D, 3rd is C.  
Then the time C walks $$t$$, then A walks $$t+2u+2x$$ (she returns). So we have the equation:
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
\end{equation}
$$


