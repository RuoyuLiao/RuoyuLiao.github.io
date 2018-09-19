---
layout: post
title: startup file in Matlab
tags: Matlab
---

Under the root directory of `Matlab`, a file called `startup.m` or `startupsav.m`. When `Matlab` is started, the scripts in `startup.m` will automatically executed. Thus we could do a great deal of things with it.

The description from `Matlab` of this file is:
>Create a startup.m file in the userpath folder, which is on the MATLAB® search path. Add commands you want executed at startup. For example, your startup function might include physical constants, defaults for graphics properties, engineering conversion factors, or anything else you want predefined in your workspace.

Here's an example of my own `startup.m` file, including the working directories assignment, font size, font name, and line width for figures, interpreter for the texts, as well as the default axes color orders.

``` Matlab
%STARTUPSAV   Startup file
%   Change the name of this file to STARTUP.M. The file
%   is executed when MATLAB starts up, if it exists
%   anywhere on the path.  In this example, the
%   MAT-file generated during quitting using FINISHSAV
%   is loaded into MATLAB during startup.

%   Copyright 1984-2000 The MathWorks, Inc.

% load matlab.mat
cd /Users/roy/Documents/MATLAB
addpath(genpath('/Users/roy/Documents/MATLAB'))
rmpath(genpath('/Users/roy/Documents/MATLAB/fun/SPECTRUM'))
rmpath(genpath('/Users/roy/Documents/MATLAB/fun/KalmanAll'))

fontSize = 12;
fontName = 'Helvetica';
lineWidth = 1;
set(0, 'defaultFigureWindowStyle', 'docked');
set(0, 'defaultAnimatedlineLineWidth', lineWidth, ...
    'defaultArrowshapeLineWidth', lineWidth, ...
    'defaultLineLineWidth', lineWidth, ...
    'defaultAxesFontName', fontName, ...
    'defaultColorBarFontName', fontName, ...
    'defaultLegendFontName', fontName, ...
    'defaultTextFontName', fontName, ...
    'defaultAxesFontSize', fontSize, ...
    'defaultColorBarFontSize', fontSize, ...
    'defaultLegendFontSize', fontSize, ...
    'defaultTextFontSize', fontSize, ...
    'defaultAxesLabelFontSizeMultiplier', 1.1, ...
    'defaultAxesTitleFontSizeMultiplier', 1.1, ...
    'defaultAxesColor', [0.95, 0.95, 0.95]);

% set(0, 'defaultAxesTickLabelInterpreter', 'Latex', ...
%     'defaultColorbarTickLabelInterpreter', 'Latex', ...
%     'defaultLegendInterpreter', 'Latex', ...
%     'defaultTextInterpreter', 'Latex');

load('colorBrewer.mat')
set(0, 'defaultAxesColorOrder', qualitative.Set.a)
clear; clc
```
