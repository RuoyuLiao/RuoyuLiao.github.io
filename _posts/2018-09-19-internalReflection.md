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

<pre style='color:#000000;background:#ffffff;'><span style='color:#bb7977; '>clear</span>
close <span style='color:#bb7977; '>all</span><span style='color:#808030; '>;</span>
clc

r <span style='color:#808030; '>=</span> 1<span style='color:#808030; '>;</span>
theta <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>linspace</span><span style='color:#808030; '>(</span>0<span style='color:#808030; '>,</span> 2<span style='color:#808030; '>*</span><span style='color:#bb7977; '>pi</span><span style='color:#808030; '>,</span> 2<span style='color:#808030; '>^</span>8<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
n1 <span style='color:#808030; '>=</span> 1<span style='color:#808030; '>;</span>
n2 <span style='color:#808030; '>=</span> <span style='color:#008000; '>1.33</span><span style='color:#808030; '>;</span>

fig <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>figure</span><span style='color:#808030; '>(</span><span style='color:#800080; '>'color'</span><span style='color:#808030; '>,</span> <span style='color:#800080; '>'k'</span><span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
Alpha <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>linspace</span><span style='color:#808030; '>(</span><span style='color:#008000; '>0.55</span><span style='color:#808030; '>*</span><span style='color:#bb7977; '>pi</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0.95</span><span style='color:#808030; '>*</span><span style='color:#bb7977; '>pi</span><span style='color:#808030; '>,</span> 50<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>

writer <span style='color:#808030; '>=</span> VideoWriter<span style='color:#808030; '>(</span><span style='color:#800080; '>'internalReflection.mp4'</span><span style='color:#808030; '>,</span> <span style='color:#800080; '>'MPEG-4'</span><span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
writer<span style='color:#808030; '>.</span>FrameRate <span style='color:#808030; '>=</span> 10<span style='color:#808030; '>;</span>
open<span style='color:#808030; '>(</span>writer<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
<span style='color:#800000; font-weight:bold; '>for</span> iLoop <span style='color:#808030; '>=</span> 1<span style='color:#808030; '>:</span><span style='color:#bb7977; '>length</span><span style='color:#808030; '>(</span>Alpha<span style='color:#808030; '>)</span>
    alpha <span style='color:#808030; '>=</span> Alpha<span style='color:#808030; '>(</span>iLoop<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
    theta_1 <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>pi</span> <span style='color:#808030; '>-</span> alpha<span style='color:#808030; '>;</span>
    theta_2 <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>asin</span><span style='color:#808030; '>(</span>n1 <span style='color:#808030; '>*</span> <span style='color:#bb7977; '>sin</span><span style='color:#808030; '>(</span>theta_1<span style='color:#808030; '>)</span> <span style='color:#808030; '>/</span> n2<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
    
    kSlope_r <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>tan</span><span style='color:#808030; '>(</span><span style='color:#bb7977; '>pi</span> <span style='color:#808030; '>-</span> <span style='color:#808030; '>(</span>theta_1 <span style='color:#808030; '>-</span> theta_2<span style='color:#808030; '>)</span><span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
    
    syms x y
    <span style='color:#808030; '>[</span>Sx<span style='color:#808030; '>,</span> Sy<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> solve<span style='color:#808030; '>(</span>x<span style='color:#808030; '>^</span>2<span style='color:#808030; '>+</span>y<span style='color:#808030; '>^</span>2<span style='color:#808030; '>=</span><span style='color:#808030; '>=</span>1<span style='color:#808030; '>,</span> <span style='color:#808030; '>(</span>x<span style='color:#808030; '>-</span><span style='color:#bb7977; '>cos</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>)</span> <span style='color:#808030; '>*</span> kSlope_r  <span style='color:#808030; '>=</span><span style='color:#808030; '>=</span> <span style='color:#808030; '>(</span>y<span style='color:#808030; '>-</span><span style='color:#bb7977; '>sin</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>)</span><span style='color:#808030; '>,</span> x<span style='color:#808030; '>,</span> y<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
<span style='color:#696969; '>%     Sx = Sx(Sx~=cos(alpha));</span>
<span style='color:#696969; '>%     Sy = Sy(Sy~=sin(alpha));</span>
    
    <span style='color:#bb7977; '>beta</span> <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>atan2</span><span style='color:#808030; '>(</span>Sy<span style='color:#808030; '>,</span> Sx<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
    <span style='color:#bb7977; '>beta</span> <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>beta</span><span style='color:#808030; '>(</span><span style='color:#bb7977; '>abs</span><span style='color:#808030; '>(</span><span style='color:#bb7977; '>beta</span> <span style='color:#808030; '>-</span> alpha<span style='color:#808030; '>)</span> <span style='color:#808030; '>></span> <span style='color:#008000; '>0.1</span><span style='color:#808030; '>*</span><span style='color:#bb7977; '>pi</span><span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
    
    <span style='color:#696969; '>% theta_i = theta_2;</span>
    <span style='color:#696969; '>% theta_t = asin(n2*sin(theta_i)/n1);</span>
    <span style='color:#696969; '>% kSlope_t = tan(beta + pi - theta_t);</span>
    clf
    <span style='color:#bb7977; '>plot</span><span style='color:#808030; '>(</span><span style='color:#bb7977; '>cos</span><span style='color:#808030; '>(</span>theta<span style='color:#808030; '>)</span><span style='color:#808030; '>,</span> <span style='color:#bb7977; '>sin</span><span style='color:#808030; '>(</span>theta<span style='color:#808030; '>)</span><span style='color:#808030; '>,</span> <span style='color:#800080; '>'y'</span><span style='color:#808030; '>)</span>                                         <span style='color:#696969; '>% the water drop (round)</span>
    <span style='color:#bb7977; '>hold</span> on
    <span style='color:#bb7977; '>plot</span><span style='color:#808030; '>(</span><span style='color:#808030; '>[</span><span style='color:#bb7977; '>cos</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>-</span><span style='color:#008000; '>0.5</span><span style='color:#808030; '>,</span> <span style='color:#bb7977; '>cos</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>]</span><span style='color:#808030; '>,</span> <span style='color:#808030; '>[</span><span style='color:#bb7977; '>sin</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>,</span> <span style='color:#bb7977; '>sin</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>]</span><span style='color:#808030; '>,</span> <span style='color:#800080; '>'w'</span><span style='color:#808030; '>)</span>         <span style='color:#696969; '>% incident</span>
    quiver<span style='color:#808030; '>(</span><span style='color:#bb7977; '>cos</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>-</span><span style='color:#008000; '>0.5</span><span style='color:#808030; '>,</span> <span style='color:#bb7977; '>sin</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0.5</span><span style='color:#808030; '>,</span> 0<span style='color:#808030; '>,</span> 0<span style='color:#808030; '>,</span> <span style='color:#800080; '>'w'</span><span style='color:#808030; '>,</span> <span style='color:#800080; '>'lineWidth'</span><span style='color:#808030; '>,</span> 2<span style='color:#808030; '>)</span>
    
    dtheta <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>beta</span> <span style='color:#808030; '>-</span> alpha<span style='color:#808030; '>;</span>
    <span style='color:#800000; font-weight:bold; '>for</span> iD <span style='color:#808030; '>=</span> 1<span style='color:#808030; '>:</span>10
        <span style='color:#bb7977; '>plot</span><span style='color:#808030; '>(</span><span style='color:#808030; '>[</span><span style='color:#bb7977; '>cos</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>,</span> <span style='color:#bb7977; '>cos</span><span style='color:#808030; '>(</span><span style='color:#bb7977; '>beta</span><span style='color:#808030; '>)</span><span style='color:#808030; '>]</span><span style='color:#808030; '>,</span> <span style='color:#808030; '>[</span><span style='color:#bb7977; '>sin</span><span style='color:#808030; '>(</span>alpha<span style='color:#808030; '>)</span><span style='color:#808030; '>,</span> <span style='color:#bb7977; '>sin</span><span style='color:#808030; '>(</span><span style='color:#bb7977; '>beta</span><span style='color:#808030; '>)</span><span style='color:#808030; '>]</span><span style='color:#808030; '>,</span> <span style='color:#800080; '>'w'</span><span style='color:#808030; '>)</span>           <span style='color:#696969; '>% refractive</span>
        alpha <span style='color:#808030; '>=</span> <span style='color:#bb7977; '>beta</span><span style='color:#808030; '>;</span>
        <span style='color:#bb7977; '>beta</span> <span style='color:#808030; '>=</span> alpha <span style='color:#808030; '>+</span> dtheta<span style='color:#808030; '>;</span>
    <span style='color:#800000; font-weight:bold; '>end</span>
    <span style='color:#bb7977; '>axis</span> equal off
    <span style='color:#bb7977; '>axis</span><span style='color:#808030; '>(</span><span style='color:#808030; '>[</span><span style='color:#808030; '>-</span><span style='color:#008000; '>1.2</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>1.2</span><span style='color:#808030; '>,</span> <span style='color:#808030; '>-</span><span style='color:#008000; '>1.2</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>1.2</span><span style='color:#808030; '>]</span><span style='color:#808030; '>)</span>
    
    frame <span style='color:#808030; '>=</span> getframe<span style='color:#808030; '>(</span>fig<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
    writeVideo<span style='color:#808030; '>(</span>writer<span style='color:#808030; '>,</span> frame<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
<span style='color:#800000; font-weight:bold; '>end</span>
close<span style='color:#808030; '>(</span>writer<span style='color:#808030; '>)</span><span style='color:#808030; '>;</span>
</pre>

