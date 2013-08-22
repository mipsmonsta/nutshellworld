---
layout: post
title: "Twitter User Name For Octopress"
date: 2013-08-22 13:32
comments: true
categories: Blogging Octopress 
---
In the _config.yml file, you can link to twitter under *Third Party Setting*.
However I had difficulty when calling rake generate. The latter will complain that the
token on line 71 is somehow causing parsing errors.

How I solve it is to put my username for twitter between quotes. 

<code> 
twitter_user: "johndoe"  
twitter_tweet_button: true

</code>