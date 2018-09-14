---
layout: post
title: harmonics in radio frequency spectrum
header-img: img/post-bg-rwd.jpg
tags: "fft spectrum-analyzer pulse-train"
---

Today, a problem arises for discussion in the office. For a set of pulse train, typically we think that the response on the spectrum analyzer reflects the repetition rate. As a result, the strongest signal locates around the fundamental repetition rate.

Problem is, why there's so many higher order harmonics and what's the temporal characteristics corresponding to those high harmonics signal.

Literally, I guess there's a misunderstanding here. We typically use the spectrum analyzer to detect the fundamental repetition rate, which does not mean that it only reflects the repetition rate.

From the perspective of frequency composition, a single frequency without any higher harmonics corresponds to an ideal sinusoid signal. Of course, the pulses in the pulse train does not exhibit a sinusoid-like shape. That's why we always say if you want to compose a signal with complicated shape, you should take as many frequencies as possible. To represent such a fine structured pulse train, you need not only the fundamental frequency, also the higher order harmonics.

Or maybe, it can be understood from the perspective of mode-locking. Take the minimal example, in a standing-wave cavity with two mirrors seperated by `l`, we know that the possible longitudinal modes intracavity would exhibit a wavelength fulfilling `nl=lambda*m/2`, where `n` is the refractive index and `m` is the integer numbers from 1, 2, 3, ... That will deliver frequencies at `f=mc/(2nl)`, in which `c` presents the speed of light. During the detection, all the intermediate frequency modes stand for the seperation of the longitudinal modes, which gives us radio frequencies at fundamental repetition rate, second harmonic, third harmonic and so on.


Pulse train and its signal after Fourier transform.
![image](/img/spectrumAnalyzer.jpg)

As a result, we should never just consider the spectrum analyzer an instrument to detect the repetition rate. It also reveals some more intrinsic sights in the pulse train.

Another question is, when dispersion of the medium is considered, carrier envelope offset (CEO) is introduced in the spectral domain. When the group velocity dispersion for different frequencies vary, why different frequencies are still seperated by a fix `f_rep`, instead of `f_rep(f)`, and why can we introduce a single CEO for the representation?

