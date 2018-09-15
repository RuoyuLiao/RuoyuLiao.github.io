---
layout: post
title: color plan for scientific articles
tags: "color-plan vector-graphics"
---

In order to keep all the colors I used in different softwares in accordance, I introduced a color plan in `Matlab` and `LaTeX`. These two are nowadays the main and maybe only two methods for vector graphics generation.

After checking like tens of different color plans, I have fixed my choice following these rules:
- the exact cataloger of the colors
- the most appropriate color palette.
- the relatively lower saturation

As a result, my color palettes come in two ways, one is from [ColorBrewer](http://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3), which provide a full range of colors in different theme. Another is from the `LaTeX` package [xcolor](https://en.wikibooks.org/wiki/LaTeX/Colors), which would need some more experience for the decision.

The first step is always thinking. What do you want to present and what's the relation in the data. Typically, according to the information of the data, `sequential`, `diverging`, or `qualitative` are ready for choice.

1. **Sequential schemes** are suited to ordered data that progress from low to high. Lightness steps dominate the look of these schemes, with light colors for low data values to dark colors for high data values. For example, if you have 5 curves with an `alpha` changing from 0.1 to 0.5 with a step of 0.1, sequential is maybe the best for visualization.
1. **Diverging schemes** put equal emphasis on mid-range critical values and extremes at both ends of the data range. The critical class or break in the middle of the legend is emphasized with light colors and low and high extremes are emphasized with dark colors that have contrasting hues. The most famous diverging color scheme used is the red-blue pair, like the one used in [Meep](https://meep.readthedocs.io/en/latest/). One can adopt it when you have a zero-centered data, for instance to present the electrical oscillation.
1. **Qualitative schemes** do not imply magnitude differences between legend classes, and hues are used to create the primary visual differences between classes. Qualitative schemes are best suited to representing nominal or categorical data.

Another need to mention is the colormap for pesudo-color map. Actually, this can be extended to a very complicated problem. The first lesson I learned is, never use the `jet` colormap for your figures, because it's not print-friendly. The later-developed `parula` in Matlab is much better. In `Python`, there's also a similar (or a little bit similar) colormap called `viridis`. (By the way, I'm not very into this colormap because I'm afraid of all kinds of snakes or snake-like things. I sometimes turn to `plasma`.) Although those colormaps are designed carefully suitable for both printable or E-distribution files, sometimes I would like to choose some others. For example, nearly all those colormaps are designed with a dark background, which sometimes makes the figure distinguished in a page. I have seen many figures with the originally dark-background colormap, yet truncated the colormap to be white below some certain value. Sometimes this seems nice, but most of the time, it's a little bit strange. I think the colormap used by [RP-photonics](https://www.rp-photonics.com/self_phase_modulation.html?s=ak) is a little bit better. However, when you want to show some details and add more colors into the colormap, maybe you turn back to `jet`. It's still too difficult to present the data logically while preserve as much fine structure as possible.

Maybe you have some better plan?
