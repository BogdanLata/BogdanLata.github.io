---
layout: page
title: Fiddler problems
description:
img: assets/img/3.jpg
importance: 2
category: work
---
[Fiddler Problem: Don't flip out](https://thefiddler.substack.com/p/dont-flip-out)  
We calculate the probability using a Markov process method. We define the states $$(a_1,a_2,a_3)\times (b_1,b_2,b_3)$$ and define the transition probabilities from a state to other $$p_{ij}((a_1,a_2,a_3)\times (b_1,b_2.b_3)\rightarrow (c_1,c_2,c_3)\times (d_1,d_2,d_3))$$, where each $$a,b,c,d$$ are 0 or 1.  
The tuples can be any of $$((0,0,0),(0,0,1),(0,1,0),(0,1,1),(1,0,0),(1,0,1),(1,1,0),(1,1,1))$$  
For our problem, we have 14 absorbing states, 7 when the game ends with either first player wins (corresponding to tuple (1,1,1)) and 7 when second player wins(corresponding to tuple (1,1,0)). 
We have that each transition probability is either 1/4 or 0.  
For example: $$P((0,0,1)\times (0,1,1)\rightarrow (0,1,0)\times (1,1,0))=1/4$$
$$P((0,0,1)\times (0,1,1)\rightarrow (0,1,1)\times (1,1,0))=1/4$$  
$$P((0,0,1)\times (0,1,1)\rightarrow (0,1,0)\times (1,1,1))=1/4$$  
$$P((0,0,1)\times (0,1,1)\rightarrow (0,1,1)\times (1,1,1))=1/4$$  
but $$P((0,0,1)\times (0,1,1)\rightarrow (0,0,0)\times (1,1,0))=0$$  
The transition probabilities form a transition probability matrix (t.p.m.) M that has dimension 64 x 64 and has the following form:
$$
  \begin{bmatrix}
    I & 0 \\
    R & Q \\ 
  \end{bmatrix}
  $$
 
 where $$R$$ is the 50x14 t.p.m. from the absorbing states to the non-absorbing, and the $$Q$$ is the 50x50 t.p.m. of the transient (non-absorbing) states

 Then the solution is provided by the following theorem:  
 If $$a_{ij}$$ is the probability that starting from transient state $$i$$ we reach the absorbing state $$j$$, then the matrix $$A=(a_{ij})$$ is given by:  
 $$A=(I-Q)^{-1}R$$.
 The matrix $$A$$ has dimension 50x14. It can be split into two parts $$A_1$$ with columns from 1 to 7 corresponding to reaching (1,1,1) and $$A_2$$ corresponding to reaching (1,1,0). 
 We calculate the total $$t_1$$ of all elements in matrix $$A_1$$ and respectively the total $$t_2$$ for $$A_2$$.  
 Then using the probabilities for the initial step we obtain that the probability that first player wins is $$1/8^2+7/8^2\cdot t_1$$ and the probability that second player wins is $$1/8^2+7/8^2\cdot t_2$$.  
 We obtain the first probability as 25439/71106~0.3578  and second probability as 45667/71106~0.6422.


<a name="dice"></a>  
  
[Fiddler Problem: Can You Roll the Dungeon Master’s Dice?](https://thefiddler.substack.com/p/can-you-roll-the-dungeon-masters)  
Suppose we choose $$x$$ and $$y$$ from set $$A=[4,6,8,10,12,20]$$. We find minimum of them, $$\min(x,y)$$. Then the probability to pick two equal numbers is:  
$$
\begin{equation}
\sum_{(x,y)\in A\times A}\frac{\min(x,y)}{36\cdot x \cdot y}=\frac{3}{32}\sim 0.09375
\end{equation}, $$
since we have 36 pairs.  
**Extra Credit** Suppose we pick a tuple $$(x,y,z)\in A\times A\times A$$. Then we sort $$(x,y,z)$$ to get $$(a,b,c)$$, where $$a\leq b\leq c$$. Now we cast the dice $$x,y,z$$ to obtain three values. The probability that all three values are equal is:
$$\begin{equation}
p_1=\sum_{(x,y,z)\in A\times A\times A}\frac{a}{216xyz}=\frac{32753}{3110400}\sim 0.01053
\end{equation} $$  
The probability that all three values are different is:  
$$
\begin{equation}
p_3=\sum_{(x,y,z)\in A\times A\times A}\frac{a(b-1)(c-2)}{216xyz}=\frac{1150553}{1555200}\sim 0.73981
\end{equation} \notag $$

The probability that only two values are different out of three is :$$p_2=1-p_1-p_3$$.    
Therefore the expectation of the number of different values is:    
$$E=p_1+2\cdot p_2+3\cdot p_3=\frac{8489153}{3110400}\sim 2.72928$$.

<details>
<summary>
  Python program
</summary>  
   

<pre><code>
 ```python   
import numpy as np;import random  
from decimal import Decimal, getcontext  
from fractions import Fraction
from myscript import List,dec
A = [4, 6, 8, 10, 12, 20]
p = [(x, y,min(x,y),Fraction(1,36)*Fraction(min(x,y),(x*y))) for x in A for y in A]
p=np.array(p)
w=sum(p[:,3]);print(w)
print(dec(w)
q=[(x,y,z,pr,Fraction(min(x,y,z),216*x*y*z),Fraction(pr)) for x in A for y in A for z in A
   if ((o:=List(sorted([x,y,z]))) and (pr:=Fraction(o[1]*(o[2]-1)*(o[3]-2),(x*y*z)*216)))]
q=np.array(q)
q1=sum(q[:,4]);print(q1);print(dec(q1))
q3=sum(q[:,5]);print(q3);print(dec(q3))
q2=1-q1-q3;print(q2);print(q1+2*q2+3*q3);print(dec(q2))
```
</code></pre>




</details>

<a name="superbowl"></a>  
  
[Fiddler On the Roof Problem:Could You Have Won the Super Bowl?](https://thefiddler.substack.com/p/could-you-have-won-the-super-bowl)  
Let's call your own team A and opponent team B. The probability team A can win in the first two times is:  
$$ P(A=7)*P(B=0 \mbox{ or } B=3)+P(A=3)*P(B=0)=1/3*2/3+1/3*1/3=1/3 $$ However A can win in the subsequent times if they draw up to this point. The probability they draw in the first two times is $$1/3*1/3+1/3*1/3+1/3*1/3=1/3$$. And the probability A wins later on is $$2/3+1/9*2/3+1/9^2*2/3+\ldots =2/3*9/8=3/4$$  
Hence, overall, A wins with probability: $$ 1/3+1/3*3/4=1/3+1/4=7/12\sim 0.583(3) $$  
**Extra Credit**  
The teams have to choose between scenarious (7 3 0) and (7 0). B knows the score after first part of game, so it can adjust its strategy accordingly. We have the followinng cases:  
1a) if A chooses (7 0) and scores a 7, B clearly chooses (7 0). Then $$P(A \mbox{ wins}|A=7)=1/2+1/2*3/4=1/2*7/4=7/8$$  
1b)  if A chooses (7 0) and instead A scores a 0, if B chooses (7 0), then B wins with probability $$ P(B=7)+P(B=0)*1/4=1/2+1/2*1/4=1/2*5/4=5/8 $$. 
If instead, B chooses (7 3 0), B wins with probability of $$2/3+1/3*1/4=2/3+1/12=9/12=3/4>5/8$$. Therefore, B opts for the better alternative (7 3 0). In this case, $$P(A \mbox{ wins}|A=0)=1-3/4=1/4$$  
Hence, overall, if A chooses (7,0), its probability of winning is $$P(A=7)*P(A \mbox{ wins}|A=7)+P(A=0)*P(A \mbox{ wins}|A=0)$$   $$=1/2*7/8+1/2*1/4=7/16+2/16=9/16= 0.5625$$  
2a) if A chooses (7 3 0)  and scores a 7, B chooses (7 0) and A wins with probability 7/8, just as in case 1a)  
2b) if A chooses (7 3 0) and scores a 3, if B chooses (7 0), B wins with probability $$1/2$$. If B chooses (7 3 0), it wins with probability $$1/3+1/3*1/4=1/3*5/4=5/12<1/2$$. Hence B opts for the better (7 0). Then A wins with probability $$1/2$$  
2c) if A chooses (7 3 0) and scores a 0, B chooses (7 3 0). In this case, A wins with probability 1/4, just in case 1b).  
So overall, if A chooses (7 3 0), its probability of winning is $$P(A=7)*P(A \mbox{ wins}|A=7)+P(A=3)*P(A \mbox{ wins}|A=3)$$   $$+P(A=0)*P(A \mbox{ wins}|A=0)=1/3*7/8+1/3*1/2+1/3*1/4=13/24= 0.541(6) $$.  
In conclusion, since A wants to optimize its way of winning, it will therefore want the stategy (7 0), in which case its chance of winning is 0.5625.  




{% comment %}
Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}

{% endcomment %}
