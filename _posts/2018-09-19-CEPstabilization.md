---
layout: post
title: CEP stabilization for ultrashort pulses
tags: Matlab CEP ultrashort-pulses
---

Below is some visualizations illustrating some basic idea about **carrier envelope phase (CEP)** and its stabilization. They're taken from my report in the symposium of [Max-Born-Institute](https://www.mbi-berlin.de/).

Due to the existence of dispersion, when a ultrashort pulse is propagating in medium, the pulse envelope and the phase plane will traveling in different velocity. The pulse envelope propagates with the speed of **group velocity**, while the phase plane is proceeding at the speed of **phase velocity**. Typically, these two are not identical. For example, when I was sitting on top of the pulse envelope (represented by the black dot), I will see the phase plane (red dot) leave me further and further.

![the difference between group velocity and phase velocity](https://ws2.sinaimg.cn/large/006tNbRwgy1fvg1d7ekzeg30go055gwu.gif)

After a short distance, the phase plane will advance the pulse envelope by an offset, which is called **group phase offset**, and the fractional part is called **carrier envelope offset (CEO)**. 

![carrier envelope phase](https://ws1.sinaimg.cn/large/006tNbRwgy1fvfjuod9a6j315u0c3gnw.jpg)

For an optical oscillator continuously outputting ultrashort pulses, all the dispersive elements intracavity will contribute to the **carrier envelope phase (CEP)**. For instance, an Ti:sapphire with a repetition rate of 100-MHz, the 4-mm Ti:S crystal and 3-m-long air will give rise to a group phase offset more than 100-cycle. As we mentioned before, we do not care the large integer number while only the fractional part really matters.

![CEP evolution intracavity](https://ws4.sinaimg.cn/large/006tNbRwgy1fvg1dohogkg30go0577f2.gif)

As a result, the output pulses will show shot-to-shot difference. Below shows a pulse train with `pi/4` CEP. The pulse is totally reversed after 4 pulses and we would expect it to repeat itself every 8 pulses.
![pulse train with pi/4 CEP](https://ws4.sinaimg.cn/large/006tNbRwgy1fvfjuly07oj30xq0ch0x1.jpg)

Taking Fourier transform on a series of pulse train with equal separation, we will obtain the a spectrum with equal-distant comb lines. The separation of the comb lines is exactly the repetition rate frequency `f_rep`. For a pulse train with identical electrical oscillation, which means the CEP is equal to 0, this optical frequency comb starts from zero frequency, shown as below.
![CEO = 0](https://ws2.sinaimg.cn/large/006tNbRwgy1fvfjuhiry6j31130iv76p.jpg)

However, if the pulses in the pulse train is not identical in electrical oscillation, when the CEP is not zero, the optical frequency comb will start from a radio frequency `f_CEO` instead of zero. We call this frequency **carrier envelope offset frequency**.
![CEO ne 0](https://ws1.sinaimg.cn/large/006tNbRwgy1fvfjudhayzj311b0ivtbe.jpg)

Typically we use self reference method for the CEO measurement, among which f-2f is the most widely-used. A prerequisite is you first got a spectrum spanning across an octave. The f component is frequency doubled to interfere with the original 2f component. The beat signal in between is exactly `f_CEO`.
![self reference method](https://ws4.sinaimg.cn/large/006tNbRwgy1fvfjuyizsuj30od0dpabw.jpg)

Most of the time, the detected `f_CEO` signal is not localized to a fixed point, instead, it vibrate in a small range, because it's always contaminated by different kinds of noise sources.
![unstabilized pulse](https://ws3.sinaimg.cn/large/006tNbRwgy1fvg1d1dloeg30go0ab4qr.gif)

With the help of **phase locked loop (PLL)**, we're able to stabilize the radio frequency of `f_CEO`, equivalent to phase lock the `CEP`. And the pulse train after phase locked is shown below. In the left, the `f_CEO` is stabilized, yet not at zero frequency, instead, to a fractional part of the repetition rate frequency, here `f_CEO=f_rep/4`. The corresponding `CEP` is equal to `pi/2`. As a result, the electrical oscillation will repeat itself every 4 pulses. In the right hand, the `f_CEO` signal is stabilized to zero frequency, thus the pulses are identical shot-to-shot.
![stabilized pulse](https://ws2.sinaimg.cn/large/006tNbRwgy1fvg1dcnnr2g30go08sjzd.gif)


For some applications where the electrical oscillation matters, the `CEP` can affect a lot. For example in high harmonic generation (HHG). If the pulse train exhibits a non-zero `CEP`, the output attosecond pulses will exhibit random intensity at un-localized position in time axis.
![influence in hhg](https://ws3.sinaimg.cn/large/006tNbRwgy1fvg1bwa2i2g30go05z0zb.gif)


