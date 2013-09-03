---
layout: post
title: "Android Action Bar Tab - How to + ViewPager Integration"
date: 2013-09-03 15:07
comments: true
categories: Android Development UI
---

Now tabs are just UI pieces. It can be added by interacting with three components
1. ActionBar.TabListener
2. ActionBar itself
3. ActionBar.newTab() .... okay this is more like a method, I concede.

The implementation patterns are as such:

in `onCreate(Bundle savedInstanceState)`

	final ActionBar actionBar = getActionBar();
	
	//set the navigation mode of actionbar to
	actionBar.setNavigationMode(ActionBar.NAVIGATION_MODE_TABS);
	
	//prepare a tab listener
	ActionBar.TabListerner tabListerner = new ActionBar.TabListener(){
	
		public void onTabSelected(ActionBar.Tab tab, FragmentTransaction ft)
		{
		
		}
		
		public void onTabUnselected(ActionBar.Tab tab, FragmentTransaction ft)
		{
		
		}
	
		public void onTabReselected(ActionBar.Tab tab, FragmentTransaction ft)
		{
			
		}
	
	}
	
	actionBar.addTab(actionBar.newTab().setText("Tab1").setTabListener(tabListener));
	
For more tabs, add in more `addTab` function calls for ActionBar.

Relationships
--------------

>ActionBar is set to NAVIGATION_MODE_TABS and has
>ActionBar.Tabs whom in turns are associated with TabListerner.
		
Viewpager Integration
----------------------

In my last [post](/blog/2013/09/03/using-the-viewpager-essence/), we talked about viewpager.
If you read it up, you will see that there is no UI to select the page to show using. Let's correct that now.

We just have to modify the TabListerner code above as follows:

	...
	//prepare a tab listener
	ActionBar.TabListerner tabListerner = new ActionBar.TabListener(){
	
		public void onTabSelected(ActionBar.Tab tab, FragmentTransaction ft)
		{
			mViewPager.setCurrentItem(tab.getPosition());
		}
	...

`setCurrentItem` accepts `int position` as inputs which the tab offers. Almost like a match made in 
heaven or they are simply meant to be used together to create great apps.



	
		
