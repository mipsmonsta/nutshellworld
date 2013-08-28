---
layout: post
title: "Simple JSON Array to string"
date: 2013-08-28 19:22
comments: true
categories: Android JSON
---

Supposed you have the following json array

<code>{"apple":"twelve", "banana": "three", "oranges": "five"}</code>, how do you extract the value
of "oranges" i.e. "five"?

As simple as this sounds, this took me awhile to figure using [GSON][1]. 

	JsonElement jelement = new JsonParser().parse(purchaseInfo);  				
	result = jelement.getAsJsonObject().get("oranges").getAsString();
	
Now *result* will contains the string "five". That was easy! The above was used in my Google 
App Engine app.

In English, this would be: "the array is a json object with the json object of property "oranges".
Once I have the "orange" object, give me it's string value which is "five".


[1]: http://code.google.com/p/google-gson/