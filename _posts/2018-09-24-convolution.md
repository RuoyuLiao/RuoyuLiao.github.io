---
layout: post
title: convolution and deconvolution in digital signal process
tags: Matlab convolution
---

## Convolution

Convolution, in mathematics and signal processing, is a “shift-and-multiply” operation performed on two signals, which involves multiplying one signal point-by-point by a delayed version of another signal, integrating or averaging the product, and repeating the process for different delays. (See a YouTube animation). It is a useful process because it accurately describes some effects that occur widely in scientific measurements, such as the influence of a low-pass filter on an electrical signal or of the resolution of an optical spectrometer on the shape of the recorded optical spectrum.
The calculation is often performed by multiplying the two signals point-by-point in the Fourier domain. First, the Fourier transform of each signal is obtained. Then the two Fourier transforms are


## Deconvolution

Deconvolution is the converse of convolution in the sense that division is the converse of multiplication. If you know that m x equals n, where m and n are known but x is unknown, then x equals n/m. Similarly, if you know that m convoluted with x equals n, where m and n are known but x is unknown, then x equals m deconvoluted from n. In practice, the deconvolution of one signal from another is usually performed by point-by-point division of the two signals in the Fourier domain - dividing the Fourier transforms of the two signals and then inverse-transforming the result.

The practical significance of deconvolution is that it can be used as an artificial (i.e. computational) way to reverse the result of a convolution occurring in the physical domain, for example, to reverse the signal distortion effect of an electrical filter or of the finite resolution of an optical spectrometer. Two different examples of the application of deconvolution are shown in the figures below.
