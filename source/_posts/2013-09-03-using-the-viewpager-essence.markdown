---
layout: post
title: "Using the ViewPager - Essence"
date: 2013-09-03 13:59
comments: true
categories: Android Development
---
For one of the project that I am currently working on, I plan to use the viewpager to swipe to 
"pages" of fragment. The key steps are planned below for implementation.

Set-up Host Activity's Layout
------------------------------

The layout file needs to include a xml viewpager. Notice this is available in the support library.
The viewpager is also occupying the full screen except for the status bar chrome.
	
	<android.support.v4.view.ViewPager
     android:id="@+id/viewpager"
     android:layout_width="fill_parent"
     android:layout_height="fill_parent" />
     
Changes to Host Activity
-------------------------

The host activity would need to be inherited from FragmentActivity (I take it because of the use
of the support library).

This activity will also need to hold on to an instance of a subclassed PageAdapter. In the 
`onCreate(Bundle savedInstanceState)`, we can find the viewpager from the activity's layout and 
then set the adapter to the instance of PageAdapter.

	...
	ViewPager pager = (ViewPager)findViewById(R.id.viewpager);
	List<Fragment> fragments = getFragments();
	pageAdapter = new SubClassdPageAdapter(getSupportFragmentManager(), fragments);
	pager.setAdapter(pageAdapter);
	
<a href id="getFragments"></a>
Notice the instantization of the pageAdapter included steps to feed it the supportFragmentManager and a
list of fragments that each will be the "page".

Declaration of the Subclassed Page Adapter
-------------------------------------------

	class SubClassedPageAdapter extends FragmentPagerAdapter {
	
		private List<Fragment> fragments;
		
		public SubClassedPageAdapter(FragmentManager fm, List<Fragment> fragments)
		{
			super(fm);
			this.fragments = fragments;
		}
		
		@Override
		public Fragment getItem(int position)
		{
			return this.fragments.get(position);
		}
		
		public int getCount()
		{
			return fragments.size();
		}
		
	}

The focus to note is the contructor which takes in the support fragment manager and a list of fragments.
The other things to note are the `getItem(int position)` and `getCount()` since these are abstract
to begin with. The job of the PagerAdapter is just to act as the intermediary to return the 
right fragments to the viewpager.


"Flow" of fragments
------------------
ViewPager <----(right fragment)----PageAdapter<-----List of Fragments 
	
Relationships
------------
	
+ViewPager has an adapter of PageAdapter. 
+PageAdapter contains a list of fragments.
	
Getting the list of Fragments
-----------------------------
Recall the `getFragments()` [function](#getFragments) call in the main activity in `onCreate`?
We just need to implement it to have our working viewpager workflow.

	...in main activity's code
	List<Fragment> getFragments()
	{
		List<Fragment> result = new ArrayList<Fragment>();
		
		Fragment frag1 = Fragment.newInstance();
		result.add(frag1);
		Fragment frag2 = Fragment.newInstance();
		result.add(frag2);
	}
	
The final bit is to integrate with actionBar tabs. But I should leave it as the next post to talk about tabs.
