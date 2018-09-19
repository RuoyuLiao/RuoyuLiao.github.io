---
layout: post
title: visualization of internal reflection in a waterdrop
tags: Matlab
---

Consider there's a perfectly round waterdrop, an incident light with different angle will result in different light path.

Or maybe more realistic, consider a light beam goes into a multi-pass ring cavity.

Below is the animated `.gif` file and the `Matlab` code snippet.

![internal reflection in a waterdrop](https://ws4.sinaimg.cn/large/006tNbRwgy1fvf65cjsb4g30go08s4ah.gif)

<pre style='color:#000020;background:#f6f8ff;'><span style='color:#7779bb; '>clear</span>
close <span style='color:#7779bb; '>all</span><span style='color:#308080; '>;</span>
clc

r <span style='color:#308080; '>=</span> 1<span style='color:#308080; '>;</span>
theta <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>linspace</span><span style='color:#308080; '>(</span>0<span style='color:#308080; '>,</span> 2<span style='color:#308080; '>*</span><span style='color:#7779bb; '>pi</span><span style='color:#308080; '>,</span> 2<span style='color:#308080; '>^</span>8<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
n1 <span style='color:#308080; '>=</span> 1<span style='color:#308080; '>;</span>
n2 <span style='color:#308080; '>=</span> <span style='color:#008000; '>1.33</span><span style='color:#308080; '>;</span>

fig <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>figure</span><span style='color:#308080; '>(</span><span style='color:#406080; '>'color'</span><span style='color:#308080; '>,</span> <span style='color:#406080; '>'k'</span><span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
Alpha <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>linspace</span><span style='color:#308080; '>(</span><span style='color:#008000; '>0.55</span><span style='color:#308080; '>*</span><span style='color:#7779bb; '>pi</span><span style='color:#308080; '>,</span> <span style='color:#008000; '>0.95</span><span style='color:#308080; '>*</span><span style='color:#7779bb; '>pi</span><span style='color:#308080; '>,</span> 50<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>

writer <span style='color:#308080; '>=</span> VideoWriter<span style='color:#308080; '>(</span><span style='color:#406080; '>'internalReflection.mp4'</span><span style='color:#308080; '>,</span> <span style='color:#406080; '>'MPEG-4'</span><span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
writer<span style='color:#308080; '>.</span>FrameRate <span style='color:#308080; '>=</span> 10<span style='color:#308080; '>;</span>
open<span style='color:#308080; '>(</span>writer<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
<span style='color:#200080; font-weight:bold; '>for</span> iLoop <span style='color:#308080; '>=</span> 1<span style='color:#308080; '>:</span><span style='color:#7779bb; '>length</span><span style='color:#308080; '>(</span>Alpha<span style='color:#308080; '>)</span>
    alpha <span style='color:#308080; '>=</span> Alpha<span style='color:#308080; '>(</span>iLoop<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
    theta_1 <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>pi</span> <span style='color:#308080; '>-</span> alpha<span style='color:#308080; '>;</span>
    theta_2 <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>asin</span><span style='color:#308080; '>(</span>n1 <span style='color:#308080; '>*</span> <span style='color:#7779bb; '>sin</span><span style='color:#308080; '>(</span>theta_1<span style='color:#308080; '>)</span> <span style='color:#308080; '>/</span> n2<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
    
    kSlope_r <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>tan</span><span style='color:#308080; '>(</span><span style='color:#7779bb; '>pi</span> <span style='color:#308080; '>-</span> <span style='color:#308080; '>(</span>theta_1 <span style='color:#308080; '>-</span> theta_2<span style='color:#308080; '>)</span><span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
    
    syms x y
    <span style='color:#308080; '>[</span>Sx<span style='color:#308080; '>,</span> Sy<span style='color:#308080; '>]</span> <span style='color:#308080; '>=</span> solve<span style='color:#308080; '>(</span>x<span style='color:#308080; '>^</span>2<span style='color:#308080; '>+</span>y<span style='color:#308080; '>^</span>2<span style='color:#308080; '>=</span><span style='color:#308080; '>=</span>1<span style='color:#308080; '>,</span> <span style='color:#308080; '>(</span>x<span style='color:#308080; '>-</span><span style='color:#7779bb; '>cos</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>)</span> <span style='color:#308080; '>*</span> kSlope_r  <span style='color:#308080; '>=</span><span style='color:#308080; '>=</span> <span style='color:#308080; '>(</span>y<span style='color:#308080; '>-</span><span style='color:#7779bb; '>sin</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>)</span><span style='color:#308080; '>,</span> x<span style='color:#308080; '>,</span> y<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
<span style='color:#595979; '>%     Sx = Sx(Sx~=cos(alpha));</span>
<span style='color:#595979; '>%     Sy = Sy(Sy~=sin(alpha));</span>
    
    <span style='color:#7779bb; '>beta</span> <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>atan2</span><span style='color:#308080; '>(</span>Sy<span style='color:#308080; '>,</span> Sx<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
    <span style='color:#7779bb; '>beta</span> <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>beta</span><span style='color:#308080; '>(</span><span style='color:#7779bb; '>abs</span><span style='color:#308080; '>(</span><span style='color:#7779bb; '>beta</span> <span style='color:#308080; '>-</span> alpha<span style='color:#308080; '>)</span> <span style='color:#308080; '>></span> <span style='color:#008000; '>0.1</span><span style='color:#308080; '>*</span><span style='color:#7779bb; '>pi</span><span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
    
    <span style='color:#595979; '>% theta_i = theta_2;</span>
    <span style='color:#595979; '>% theta_t = asin(n2*sin(theta_i)/n1);</span>
    <span style='color:#595979; '>% kSlope_t = tan(beta + pi - theta_t);</span>
    clf
    <span style='color:#7779bb; '>plot</span><span style='color:#308080; '>(</span><span style='color:#7779bb; '>cos</span><span style='color:#308080; '>(</span>theta<span style='color:#308080; '>)</span><span style='color:#308080; '>,</span> <span style='color:#7779bb; '>sin</span><span style='color:#308080; '>(</span>theta<span style='color:#308080; '>)</span><span style='color:#308080; '>,</span> <span style='color:#406080; '>'y'</span><span style='color:#308080; '>)</span>                                         <span style='color:#595979; '>% the water drop (round)</span>
    <span style='color:#7779bb; '>hold</span> on
    <span style='color:#7779bb; '>plot</span><span style='color:#308080; '>(</span><span style='color:#308080; '>[</span><span style='color:#7779bb; '>cos</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>-</span><span style='color:#008000; '>0.5</span><span style='color:#308080; '>,</span> <span style='color:#7779bb; '>cos</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>]</span><span style='color:#308080; '>,</span> <span style='color:#308080; '>[</span><span style='color:#7779bb; '>sin</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>,</span> <span style='color:#7779bb; '>sin</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>]</span><span style='color:#308080; '>,</span> <span style='color:#406080; '>'w'</span><span style='color:#308080; '>)</span>         <span style='color:#595979; '>% incident</span>
    quiver<span style='color:#308080; '>(</span><span style='color:#7779bb; '>cos</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>-</span><span style='color:#008000; '>0.5</span><span style='color:#308080; '>,</span> <span style='color:#7779bb; '>sin</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>,</span> <span style='color:#008000; '>0.5</span><span style='color:#308080; '>,</span> 0<span style='color:#308080; '>,</span> 0<span style='color:#308080; '>,</span> <span style='color:#406080; '>'w'</span><span style='color:#308080; '>,</span> <span style='color:#406080; '>'lineWidth'</span><span style='color:#308080; '>,</span> 2<span style='color:#308080; '>)</span>
    
    dtheta <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>beta</span> <span style='color:#308080; '>-</span> alpha<span style='color:#308080; '>;</span>
    <span style='color:#200080; font-weight:bold; '>for</span> iD <span style='color:#308080; '>=</span> 1<span style='color:#308080; '>:</span>10
        <span style='color:#7779bb; '>plot</span><span style='color:#308080; '>(</span><span style='color:#308080; '>[</span><span style='color:#7779bb; '>cos</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>,</span> <span style='color:#7779bb; '>cos</span><span style='color:#308080; '>(</span><span style='color:#7779bb; '>beta</span><span style='color:#308080; '>)</span><span style='color:#308080; '>]</span><span style='color:#308080; '>,</span> <span style='color:#308080; '>[</span><span style='color:#7779bb; '>sin</span><span style='color:#308080; '>(</span>alpha<span style='color:#308080; '>)</span><span style='color:#308080; '>,</span> <span style='color:#7779bb; '>sin</span><span style='color:#308080; '>(</span><span style='color:#7779bb; '>beta</span><span style='color:#308080; '>)</span><span style='color:#308080; '>]</span><span style='color:#308080; '>,</span> <span style='color:#406080; '>'w'</span><span style='color:#308080; '>)</span>           <span style='color:#595979; '>% refractive</span>
        alpha <span style='color:#308080; '>=</span> <span style='color:#7779bb; '>beta</span><span style='color:#308080; '>;</span>
        <span style='color:#7779bb; '>beta</span> <span style='color:#308080; '>=</span> alpha <span style='color:#308080; '>+</span> dtheta<span style='color:#308080; '>;</span>
    <span style='color:#200080; font-weight:bold; '>end</span>
    <span style='color:#7779bb; '>axis</span> equal off
    <span style='color:#7779bb; '>axis</span><span style='color:#308080; '>(</span><span style='color:#308080; '>[</span><span style='color:#308080; '>-</span><span style='color:#008000; '>1.2</span><span style='color:#308080; '>,</span> <span style='color:#008000; '>1.2</span><span style='color:#308080; '>,</span> <span style='color:#308080; '>-</span><span style='color:#008000; '>1.2</span><span style='color:#308080; '>,</span> <span style='color:#008000; '>1.2</span><span style='color:#308080; '>]</span><span style='color:#308080; '>)</span>
    
    frame <span style='color:#308080; '>=</span> getframe<span style='color:#308080; '>(</span>fig<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
    writeVideo<span style='color:#308080; '>(</span>writer<span style='color:#308080; '>,</span> frame<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
<span style='color:#200080; font-weight:bold; '>end</span>
close<span style='color:#308080; '>(</span>writer<span style='color:#308080; '>)</span><span style='color:#308080; '>;</span>
</pre>

