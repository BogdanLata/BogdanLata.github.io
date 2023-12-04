---
layout: page
title: Problems 1
description:
img: assets/img/12.jpg
importance: 1
category: work
related_publications: 
---
{% comment %}
**The Cauchy-Schwarz Inequality**
$$\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)$$
{% endcomment %}

[Fiddler problem: Can You Race Around the Monopoly Board?](https://thefiddler.substack.com/p/can-you-race-around-the-monopoly)

The probablity to reach number $$x$$ in the $$n$$-th cast be $$p_n(x)$$. Then the probability that the number $$x$$ is hit is:  
$$ p(x)=p_1(x)+(1-p_1(x))*p_2(x)+(1-p_1(x))*(1-p_2(x))*p_3(x)+\ldots $$ Now, the probability mass function after casting two dice can be calculated from square of the generated polynomial of the p.m.f of one dice: $$ g(x)=x^6/6+x^5/6+x^4/6+x^3/6+x^2/6+x/6 $$.     
That is, $$ h(x)=g^2(x)=x^2/36 + x^3/18 + x^4/12 + x^5/9 + 5 x^6/36 + x^7/6 + $$ $$ 5 x^8/36 + x^9/9 + x^{10}/12 + x^{11}/18 + x^{12}/36 $$.     
So, for example, $$ p_2(8)=5/36 $$  
And the probability after another two-dice cast is the 4-th power of $$g$$ and so on.   
The least element of the $$ h^{20} $$ is $$ x^{40} $$ and we only are interested in the numbers $$x$$ from 1 to 39. Therefore, we only have to calculate the powers of $$h$$ from 1 to 19.    
Running the program, we obtain the extremum values for two dice case:  
(0.1796322, 7)
(0.1228949, 13)
So the maximum probability is p(7)~0.179632 and the minimum probability (out of the numbers from 10 to 39) is p(13)~0.1228949  
For the three dice case, the least likely case (out of the numbers from 10 to 39) is p(16)~0.075185  

Here is the Python code for two dice case:

```python
import numpy as np
from numpy.polynomial import Polynomial as P

p= P([0,1/6,1/6,1/6,1/6,1/6,1/6])
p=p**2    
r = []
for i in range(1, 40):
    r.append([i])

for i in range(1, 40):
    for j in range(1,20):
       q=p**j;
       if i<= q.degree():       
                         r[i-1].append(q.coef[i])
       else:
           r[i-1].append(0)

s= [row[1:] for row in r]

sum=[]
for i in range(39):
    sum.append(0);
    for j in range(19):
        product = 1
        for value in s[i][:j]:
          product *= 1-value
        product=product*s[i][j]
        sum[i]+=product
        
print(max((val, idx+1) for idx, val in enumerate(sum)))
s10=sum[10:]
print(min((val, idx+11) for idx, val in enumerate(s10)))
```


{% comment %} Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width. {% endcomment %}
{% comment %}
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
        include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" 
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

can also put regular text between your rows of images.
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

