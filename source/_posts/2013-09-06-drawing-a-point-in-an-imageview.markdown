---
layout: post
title: "Drawing a point in an ImageView"
date: 2013-09-06 15:35
comments: true
categories: Android Graphics Development 
---
Suppose you have an image that is of size 50 px by 50 px. This image will be presented in an
imageview. Now if you wanted to draw a point at exactly (30 px, 30 px) in the image coordinate space,
how would you go about it in Android.

First of all, let's talk about challenges posed by the Android framework. The size of the imageview 
may not be the same size and/or aspect as the image. Also, pre-scaling of the bitmap may be done since the 
density of the screen may be higher than what was assumed for the bitmap image. **Headache** is all.

My solution:

> In onDraw() method in a subclassed ImageView

	Matrix mat = getImageMatrix();
	
	float[] pts = {30, 30}; //in {x0, y0, x1, y1,...} format
	
	mat.mapPts(pts);
	
	float mappedX = pts[0];
	float mappedY = pts[1];
	
Now _mappedX_ and _mappedY_ will be the new coordinates for (30px, 30px) in the _new_ image coordinate space.

Cheers!