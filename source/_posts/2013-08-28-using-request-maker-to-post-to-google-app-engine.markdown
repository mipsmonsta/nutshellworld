---
layout: post
title: "Using Request Maker to Post to Google App Engine"
date: 2013-08-28 16:07
comments: true
categories: Android Networking
---

[Request Maker][1] allows you to send GET/POST/GET/PUT/DELETE request to any web url. I was particularly
interested in its ability to send Post messages to my Google App Engine app.

For example, if I want to send foo=bar&mad=man as the request body, I just have to typed
<code>foo=bar&mad=man</code> verbertim into the Request Data form input at request maker.

However, I had difficulty extracting these key-values at Google App Engine using 
the <code>request.getParameter("foo")</code> code. 

Turns out for it all to work, you need to set the request header's content-type to

>application/x-www-form-urlencoded; charset=utf-8  

That helped me and I hope it helps you.


[1]: http://www.requestmaker.com