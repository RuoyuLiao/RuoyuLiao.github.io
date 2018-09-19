---
layout: post
title: visualization of internal reflection in a waterdrop
tags: Matlab
---

![internal reflection in a waterdrop](https://ws4.sinaimg.cn/large/006tNbRwgy1fvf65cjsb4g30go08s4ah.gif)

```Matlab
clear
close all;
clc

r = 1;
theta = linspace(0, 2*pi, 2^8);
n1 = 1;
n2 = 1.33;

fig = figure('color', 'k');
Alpha = linspace(0.55*pi, 0.95*pi, 50);

writer = VideoWriter('internalReflection.mp4', 'MPEG-4');
writer.FrameRate = 10;
open(writer);
for iLoop = 1:length(Alpha)
    alpha = Alpha(iLoop);
    theta_1 = pi - alpha;
    theta_2 = asin(n1 * sin(theta_1) / n2);
    
    kSlope_r = tan(pi - (theta_1 - theta_2));
    
    syms x y
    [Sx, Sy] = solve(x^2+y^2==1, (x-cos(alpha)) * kSlope_r  == (y-sin(alpha)), x, y);
    
    beta = atan2(Sy, Sx);
    beta = beta(abs(beta - alpha) > 0.1*pi);
    
    % theta_i = theta_2;
    % theta_t = asin(n2*sin(theta_i)/n1);
    % kSlope_t = tan(beta + pi - theta_t);
    clf
    plot(cos(theta), sin(theta), 'y')                                         % the water drop (round)
    hold on
    plot([cos(alpha)-0.5, cos(alpha)], [sin(alpha), sin(alpha)], 'w')         % incident
    quiver(cos(alpha)-0.5, sin(alpha), 0.5, 0, 0, 'w', 'lineWidth', 2)
    
    dtheta = beta - alpha;
    for iD = 1:10
        plot([cos(alpha), cos(beta)], [sin(alpha), sin(beta)], 'w')           % refractive
        alpha = beta;
        beta = alpha + dtheta;
    end
    axis equal off
    axis([-1.2, 1.2, -1.2, 1.2])
    
    frame = getframe(fig);
    writeVideo(writer, frame);
end
close(writer);
```

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

