---
layout: post
title: image processing in Imagemagick
tags: Imagemagick
---

[ImageMagick](https://www.imagemagick.org/script/index.php) (IM) is a free software for image processing in command-line.

It provide several convenient way to deal with the images, as well as easy batch-operation.

Here is the most common command syntax:
```
convert "image" { -operation }... "output_image"
```
or 
```
mogrify "image" { -operation }... "output_image"
```
for batch-operation.

Here is a grocery of the operators supported, listed in the order of my preference:


- -trim
- -resize
- -crop
- -magnify
- -rotate
- -negate
- -annotate

There's actually a huge number of operators,
```
-crop  -repage  -border  -frame  -chop  -draw  -annotate  -scale  -sample  -thumbnail  -adaptive-resize  -liquid-resize  -distort  -morpohology  -sparse-color   -swirl  -implode  -wave  -flip  -flop  -transpose  -transverse  -blur  -gaussian-blur  -convolve  -shadow  --radial-blur  -motion-blur  -sharpen  -unsharp  -adaptive-sharpen  -adaptive-blur  -noise  -despeckle  -median   -level  -level-color  -gamma  -auto-level  -auto-gamma  -sigmoidial -contrast  -normalize  -linear-stretch  -contrast-stretch  -colorize  -tint  -modulate  -contrast  -equalize  -sepia-tone  -solarize  -recolor  -opaque  -transparent  -colors  -map  -ordered-dither  -random-dither  -raise  -paint  -sketch  -charcoal  -edge  -vignette  -emboss  -shade  -poloroid  -encipher  -decipher  -stegano  -evaluate  -function  -alpha  -colorspace  -separate 
```

Of course, the most commonly used for format conversion, there's no need for any other operators:
```
convert a.png a_out.jpg
```

For batch-operation, you can use some regular expression (regex) for rule match, for example:
```
convert *.jpg ./new/*.png
```
will convert all the `.jpg` files into `.png` and store into a new directory.


