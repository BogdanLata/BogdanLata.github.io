---
layout: page
title: project 2
description:
img: assets/img/3.jpg
importance: 2
category: work
---
[Fiddler Problem: Don't flip out](https://thefiddler.substack.com/p/dont-flip-out)  
We calculate the probability using a Markov process method. We define the states $$(a_1,a_2,a_3)\times (b_1,b_2,b_3)$$ and define the transition probabilities from a state to other $$p_{ij}((a_1,a_2,a_3)\times (b_1,b_2.b_3)\rightarrow (c_1,c_2,c_3)\times (d_1,d_2,d_3))$$, where each $$a,b,c,d$$ are 0 or 1.  
The tuples can be any of $${{0,0,0},{0,0,1},{0,1,0},{0,1,1},{1,0,0},{1,0,1},{1,1,0},{1,1,1}}$$  
For our problem, we have 14 absorbing states, 7 when the game ends with either first player wins (corresponding to tuple (1,1,1)) and 7 when second player wins(corresponding to tuple (1,1,0)). These absorbing states are:   
We have that each transition probability is either 1/4 or 0.  
For example: $$P((0,0,1)\times (0,1,1)\rightarrow (0,1,0)\times (1,1,0))=1/4$$
$$P((0,0,1)\times (0,1,1)\rightarrow (0,1,1)\times (1,1,0))=1/4$$  
$$P((0,0,1)\times (0,1,1)\rightarrow (0,1,0)\times (1,1,1))=1/4$$  
$$P((0,0,1)\times (0,1,1)\rightarrow (0,1,1)\times (1,1,1))=1/4$$  
but $$P((0,0,1)\times (0,1,1)\rightarrow (0,0,0)\times (1,1,0))=0$$  
The transition probabilities form a transition probability matrix (t.p.m.) M that has dimension 64 x 64 and has the following form:
{% comment %}
$${{{0,0,0},{1,1,0}},{{0,0,1},{1,1,0}},{{0,1,0},{1,1,0}},{{0,1,1},{1,1,0}},{{1,0,0},{1,1,0}},{{1,0,1},{1,1,0}},{{1,1,0},{1,1,0}},{{1,1,1},{0,0,0}},{{1,1,1},{0,0,1}},{{1,1,1},{0,1,0}},{{1,1,1},{0,1,1}},{{1,1,1},{1,0,0}},{{1,1,1},{1,0,1}},{{1,1,1},{1,1,0}},{{1,1,1},{1,1,1}}}
Out[147]= {{{0,0,0},{1,1,0}},{{0,0,1},{1,1,0}},{{0,1,0},{1,1,0}},{{0,1,1},{1,1,0}},{{1,0,0},{1,1,0}},{{1,0,1},{1,1,0}},{{1,1,0},{1,1,0}},{{1,1,1},{0,0,0}},{{1,1,1},{0,0,1}},{{1,1,1},{0,1,0}},{{1,1,1},{0,1,1}},{{1,1,1},{1,0,0}},{{1,1,1},{1,0,1}},{{1,1,1},{1,1,0}},{{1,1,1},{1,1,1}}}
{{{0,0,0},{1,1,0}},{{0,0,1},{1,1,0}},{{0,1,0},{1,1,0}},{{0,1,1},{1,1,0}},{{1,0,0},{1,1,0}},{{1,0,1},{1,1,0}},{{1,1,0},{1,1,0}},{{1,1,1},{0,0,0}},{{1,1,1},{0,0,1}},{{1,1,1},{0,1,0}},{{1,1,1},{0,1,1}},{{1,1,1},{1,0,0}},{{1,1,1},{1,0,1}},{{1,1,1},{1,1,0}},{{1,1,1},{1,1,1}}}$$
$$ {% endcomment %}

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
 Then using the probabilities for the initial step we obtain that the probability that first player wins is $$1/16^2+7/16^2\cdot t_1$$ and the probability that second player wins is $$1/16^2+7/16\cdot t_2$$.  
 We obtain the first probability as 25439/71106~0.3578  and second probability as 45667/71106~0.6422.








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
