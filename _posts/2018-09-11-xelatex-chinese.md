---
layout: post
title: 使用xelatex生成中文pdf
tags: latex xelatex chinese mac
---


一直以来编辑LaTeX中文文档都是个麻烦事，因为TeX最初的设计就没有考虑多语言问题，所以后来使用CJK这个外挂包来处理中文字体。但是，由于CJK是个中文外挂，用起来很麻烦，需要自己编译生成中文字体集，而且常常有些问题，比如，中文目录的问题就一直没能解决，总是乱码。最近，由于想把org导出成pdf，于是研究了一下。发觉一个好东西 XeTeX，在LaTeX宏包里，它被称作XeLaTeX。

为什么说是个好东西呢？因为XeTeX就是为了支持多语言而重新设计的新一代TeX系统，这意味着在XeTeX眼里，中文文档和英文文档再没有任何区别，无需额外的外挂包；而且，XeTeX原生支持系统字体，这意味着我们无需再额外编译字体，系统安装了什么字体，我们就能使用什么字体。这两大优点简直就是大家一直以来梦寐以求的功能，所有的CJK环境、pdflatex这些老工具完全都可以抛弃了，以前碰到的让人焦头烂额的字体问题，再也不会困扰我们了。可以说，使用TeX的难度至少降低了50%。


``` latex
\documentclass[12pt]{article}
\usepackage{fontspec}
\setmainfont{AR PL ShanHeiSun Uni}
\title{石頭記}
\author{曹雪芹}
\date{}

\begin{document}
\maketitle

\begin{center}
滿紙荒唐言\\
一把辛酸淚\\
都雲作者癡\\
誰解其中味\\
\end{center}

\end{document}
```

然后使用xelatex输出pdf文档:
```
$ xelatex sample.tex
```

你可以使用 `\setmainfont`, `\setsansfont` 和 `\setmonofont` 来分别设置衬线字体，无衬线字体和等宽字体。也可以把这些默认配置写入sty文件，放到 texmf 目录下，比如 `~/.texmf-config/zhfontcfg.sty`。

Mac OS X下边可以把.sty放入目录 `~/Library/texmf/tex/latex/`。

``` latex
% xetex/xelatex 字体设定宏包

\ProvidesPackage{zhfontcfg}
\usepackage{fontspec,xunicode}
\defaultfontfeatures{Mapping=tex-text} %如果没有它，会有一些 tex 特殊字符无法正常使用，比如连字符。

 % 中文断行
\XeTeXlinebreaklocale "zh"
\XeTeXlinebreakskip = 0pt plus 1pt minus 0.1pt

%将系统字体名映射为逻辑字体名称，主要是为了维护的方便。`fc-list :lang=zh` 确保字体在系统中存在。
\newcommand\fontnamehei{文泉驿正黑}
\newcommand\fontnamesong{文鼎ＰＬ新宋}
\newcommand\fontnamekai{AR PL UKai CN}
\newcommand\fontnamemono{Bitstream Vera Sans Mono}
\newcommand\fontnameroman{Bitstream Vera Serif}

%设置文档正文字体为宋体
\setmainfont{\fontnamesong}
\setsansfont[BoldFont=\fontnamekai]{\fontnamekai}
\setmonofont{\fontnamemono}

%楷体
\newfontinstance\KAI {\fontnamekai}
\newcommand{\kai}[ 1]{{\KAI #1}}

%黑体
%\newfontinstance\HEI{\fontnamehei}
%\newcommand{\hei}[ 1]{{\HEI #1}}

%英文
\newfontinstance\ENF{\fontnameroman }
\newcommand{\en}[1 ]{\,{\ENF #1 }\,}
\newcommand{\EN}{\,\ENF\, }
```

然后更新文件索引：
```
$ sudo mktexlsr
```
现在就可以在xelatex中使用zhfontcfg宏包了：
```
\usepackage{zhfontcfg}
```

输入中文：
```
\kai{这样可以输入楷体}
{\KAI 也可以这样输入楷体}
```

## 在Mac下安装xecjk

xelatex虽然能够正常使用系统字体，但是无法分别指定中英文字体，这需要借助xecjk宏包实现，也可以安装ctex宏包，但后者会依赖Windows下的字体，具体可以参考 ctex项目。

Linux下的texlive-xetex中已经包括了xecjk，但是Mac下从homebrew安装texlive的话，默认是不包括这个宏包的，可以用如下命令安装
```
$ sudo tlmgr install xecjk
```

测试一下是否工作正常：

``` latex
\documentclass[12pt,a4paper]{article}
\usepackage{xltxtra,fontspec,xunicode}
\usepackage[slantfont,boldfont]{xeCJK} % 允许斜体和粗体

\setCJKmainfont{Kai}   % 设置缺省中文字体
\setCJKmonofont{Hei}   % 设置等宽字体
\setmainfont{Optima}   % 英文衬线字体
\setmonofont{Monaco}   % 英文等宽字体
\setsansfont{Trebuchet MS} % 英文无衬线字体

\begin{document}
\begin{verse}
  Stray birds of summer come to my window to sing and fly away. \\
  And yellow leaves of autumn, which have no songs, \\
  flutter and fall there with a sign.\\
  \hfill \emph{Rabindranath Tagore}
\end{verse}

\begin{verse}
  夏天的飞鸟，飞到我的窗前唱歌，又飞去了。\\
  秋天的黄叶，它们没有什么可唱，只叹息一声，飞落在那里。\\
  \hfill \emph{罗宾德拉纳特·泰戈尔}
\end{verse}
\end{document}
```

文章转自[逍遥郡](http://blog.jqian.net/post/xelatex.html)