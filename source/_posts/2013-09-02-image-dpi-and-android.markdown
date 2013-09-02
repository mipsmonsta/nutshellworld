---
layout: post
title: "Image DPI and Android"
date: 2013-09-02 10:22
comments: true
categories: Android Graphics
---
Android developer documents states that the baseline screen density is taken to be 160 pixels (px) per
inch. If your device has 240 px per inch (high density), a image of size 100px by 100px will appear larger on the baseline
baseline screen than the high density screen. Specially, the image will be 0.625 of an inch on baseline screen compared to 
0.416 inch on the higher density screen. 

Then how does *image dpi* relates to how Android serves up the image. The answer as I have researched is __NOTHING__.
Turns out the image dpi has no bearing on how large the images are displayed on the computer or cellphone screen.
It does however specify how large these images are printed on paper. For example, two images of 100px by 100px but at different
dpi of 200 dpi and 100 dpi will look the same size on the same cellphone screen. However, when printed,
the one with the higher dpi will print as half the dimension as the other.

You can refer to this [scantips](http://www.scantips.com/no72dpi.html) for more on image dpi.

For us Android developers, we just have to stop worrying about image dpi. If only we 
can do the same for screen density...lol.

