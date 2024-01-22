---
layout: page
title: Fiddler_pancakes
description:
img: 
importance: 2
category: work
---
[Fiddler Problem: Can You Make It Home in Time for Pancakes?](https://thefiddler.substack.com/p/can-you-make-it-home-in-time-for)  
The four siblings can meet several times all four again during their walk. Wlog we assume they never meet again all four(see Discussion at the ending).  
Denote the total length L and the players A,B,C,D with speeds L/10,L/20,L/30,L/60. Player A picks a person.(1st pick) For optimization purpose, 
A will drop before home whoever she picked, so that she can go back and the dropped person can meanwhile reach the home. Player A goes back and picks another one.  
(2nd pick) Now A returns and we argue she has to drop 2nd pick to 1st pick. Because if she drops before reaching the 1st, it is not an ideal solution-
she could have dropped the 1st earlier. After this, A goes back second time and picks the 3rd. Ideally, she reaches the home at the same time with 1st and 2nd.    
So we can split the events into several parts:   
1) A drops 1st, goes back to the other two  (  time 1)  
2) picks 2nd, goes back to 1st (time 2)  
3) goes back to the last  (time 3)  
4) they all rush to home (time 4)  
This way we create several segments of the trip:    
{% raw %}Start---|---|---|---|---End {% endraw %}, and denote the lengths of these segments: $$t,u,x,y,z$$.    
Case 1) Suppose 1st is B, 2nd is D, 3rd is C.  
Then during the time C walks $$t$$, then A walks $$t+2u+2x$$ (she returns). So we have the equation:
$$
\begin{equation}
30t/L=10/L(t+2u+2x) \mbox{     time 1}
\end{equation}
$$
Similarly, we obtain the following equations:
$$
\begin{equation}
20t/L=10/L(u+x+y), \mbox{ time 2}
\end{equation} $$
$$ \begin{equation}
30t/L=10/L(u+2x+2y), \mbox{ time 2+time 3}
\end{equation} $$   
$$ \begin{equation} 20t/L=10/L(2x+2y+z), \mbox{ time 3+time 4} \end{equation} $$   
$$\begin{equation} t+u+x+y+z=L \end{equation} $$
Note that total time is $$T=$$ time 1+time 2+time 3+ time 4$$=10/L(t+3u+5x+3y+z)=10/L(L+2u+4x+2y)$$  
Solving the above system of equations we obtain $$T=$$.  
If we have other cases, note that only the right hand terms change, which are the ones corresponding to: max(2nd,3rd) (equation1), 1st (equation2), 3rd (equation 3), max(1st,2nd) (equation 4). For case 1) these were (3,2,3,2)*10.  
Case 2) (1st,2nd,3rd)=(B,C,D). This case is clearly slower than the first.  We calculate though, $$T=$$.
Case 3) (1st,2nd,3rd)=(C,B,D). Coefficients (2,3,6,2). Here, $$T=$$  
Case 4) (1st,2nd,3rd)=(C,D,B). Coefficients (2,3,2,3). Here $$T=$$  
Case 5) (1st,2nd,3rd)=(D,B,C). Coefficients (2,6,3,2). Here $$T=$$  
Case 6) (1st,2nd,3rd)=(D,C,B). Coefficients (2,6,2,3). Here $$T=$$  
In conclusion, the ideal set up is: with the time:  
**Discussion**:  
1) One can see that the solution is valid for any distance from playground to home or any intermediary distance. That is if he have, say, halved the distance, the optimal solution is the same and we just halve the time. So the solution includes the 4 siblings repeating the above procedure again and again on any intermediary distance. Naturally that can be done a finite number of times.  
2)  If there is no intermediary meeting of all 4 or of 3 of them, then the minimal time is when A, B rush to the end, in which case $T=20$.  
3) If there is no intemediary meeting of all 4 but 3 of them meet again. This case happens if A at some point drops a player and goes back for other one. An optimal way as we have seen is, in the final stage to pass a player to the leading one. So there is a final $$z$$ and an initial segment  $$t$$. The solution is given above.     


