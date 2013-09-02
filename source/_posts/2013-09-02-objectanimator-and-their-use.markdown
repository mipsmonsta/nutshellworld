---
layout: post
title: "ObjectAnimator and their use"
date: 2013-09-02 12:44
comments: true
categories: Android Development Animation
---
History
-------

Object animator was added in Android API 11 (Honeycomb i.e. 3.0). This class allows *targeting* objects (views or fragmentInstance.getView())
and animating their properties.


Use
---

	ObjectAnimator movingFragmentAnimator = ObjectAnimator.
                ofPropertyValuesHolder(<target>, <PropertyValuesHolder value>, <PropertyValuesHolder value>, ...);
                
Here you can see a static constructor that takes in *list* of PropertyValuesHolder values all
targeting the same view object.

**OR**

	ObjectAnimator darkHoverViewAnimator = ObjectAnimator.
                ofFloat(mDarkHoverView, "alpha", 0.0f, 0.5f);
               
Only one property of the target is to be animated here.

PropertyValuesHolder
--------------------

	PropertyValuesHolder rotateX =  PropertyValuesHolder.ofFloat("rotationX", 40f);
	
Here you can see that **rotationX** is the property value to change and "40f" is the degree to turn about the x-axis.

Tweaking Object Animator further <a id="tweaks"></a>
--------------------------------

Duration of the animation can be changed:

	darkHoverViewAnimator.setDuration(long millisec)
	
__Default__ duration is 300 msec according to documentation.

How about starting animation with a delay:

	darkHoverViewAnimator.startDelay(long millisec)

Starting animation of an Object animator
----------------------------------------

	darkHoverViewAnimator.start()
	
Starting animation of multiple Object Animators
-----------------------------------------------

We achieve this by using a *AnimatorSet* instance instead of calling individual objectanimator's start().

	  AnimatorSet s = new AnimatorSet();
      s.playTogether(movingFragmentAnimator, darkHoverViewAnimator, movingFragmentRotator);
      s.addListener(listener); 
      s.start();
      
The animatorset allows the simultaneous playback of all animator's animation. When each object(target) starts their animation 
depends of course on whether their startDelay property has been [set](#tweaks).

Chaining even more animations to start after
--------------------------------------------

Notice the line `s.addListener(listener)`? The class of the listener in this case is **Animator.AnimatorListener**.
An instance of this AnimatorListener allows the overriding of four methods that corresponds to 
specific instance of the animator's lifecycle.

		AnimatorListener listener = new AnimatorListenerAdapter() {
                @Override
                public void onAnimationEnd(Animator arg0) {
                    FragmentTransaction transaction = getFragmentManager().beginTransaction();
                    transaction.setCustomAnimations(R.animator.slide_fragment_in, 0, 0,
                            R.animator.slide_fragment_out);
                    transaction.add(R.id.move_to_back_container, mTextFragment);
                    transaction.addToBackStack(null);
                    transaction.commit();
                }
            };

We are only overriding the *onAnimationEnd*. There are other lifecycle events that we can also tracked:

+ onAnimationCancel
+ onAnimationStart
+ onAnimationRepeat

See [documentation for AnimatorListener to find out more][1].

In the above code, we will add a fragment in at the end of AnimatorSet's animation. Interestingly, 
doc for FragmentTransaction says

>abstract FragmentTransaction	 
>setCustomAnimations(int enter, int exit, int popEnter, int popExit)
>*Desc:* Set specific animation resources to run for the fragments that are entering and exiting in this transaction.

This means that mTextFragment will "enter" and "pop out" with the specified animation resource ids.
I suspect "popEnter" refers to the animation for the fragment beneath mTextFragment when it pops up.
We of course set this animation resource id to *"zero"*, indicating no animation at all.

Specifying Object Animator in XML in lieu of code
--------------------------------

	<objectAnimator xmlns:android="http://schemas.android.com/apk/res/android"
    	android:valueFrom="0"
    	android:valueTo="@dimen/slide_up_down_fraction"
    	android:propertyName="yFraction"
    	android:valueType="floatType"
    	android:duration="@integer/slide_up_down_duration">
	</objectAnimator>
	
The xml objectAnimator file will go under the "animator" folder. It's resource identifier will be
R.animator.<name_of_file>. 

Summary
-------
We saw how to use the following objects together or in partial isolation to achieve useful animations:
+ PropertyValuesHolder
+ ObjectAnimator
+ AnimatorSet
+ AnimatorListener. 

[1]: http://developer.android.com/reference/android/animation/Animator.AnimatorListener.html
