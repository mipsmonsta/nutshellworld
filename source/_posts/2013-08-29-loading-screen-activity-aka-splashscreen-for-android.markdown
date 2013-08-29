---
layout: post
title: "Loading Screen Activity (AKA) SplashScreen for Android"
date: 2013-08-29 17:16
comments: true
categories: Android Development
---
I was dabbling with implement *In App Purchase (IAB)*  for my Android app. According to Google documentation,
it would be best to change the UI instantly once the purchase was successful. However, this is not possible
for my app unless after a restart.

The documentation also advised to do a server query for the purchased item status every so often, preferably
everytime the app is started.

How I implemented my part of my app's IAB workflow is as such:

1. User makes the purchase, but the UI of the app will only update after the next app's start up.
2. If the User download the app on his other devices for the first time, app will need to check for his 
purchases before going into the main UI.

The above use cases led me to implement a splash screen activity that will always run before my main UI activity.
However I have some optimizing to shorten the on screen time of this splash screen. After all, who likes to wait?

Some of the design choices to cut waiting time are:

+ When the purchase transaction first came through, I would set a flag in the app to note this event. 
+ Then I forced the app to shutdown and prompt the user to *restart* the app with a Toast message.
+ At the next start-up, the splash screen `onCreate()` code will check for the presence of the flag.
	+ If the flag exists, the splashscreen quickly starts the main UI activity.
	+ If not, this start-up could be the first start up on a device that newly install the app. 
		+ So the splashscreen activity will check with Google Play Services for any purchases. In this case 
		the splash screen may dwell longer on the screen becauses of server calls.
		
To make the splash screen as unintrusive as possible, I also styled the activity using the 
`android:theme="@android:style/Theme.Dialog` in the application manifest.


		
