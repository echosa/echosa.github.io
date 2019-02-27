---
layout: post
title: "Changing the REST of My Life"
date: 2012-07-13 14:53
comments: true
tags:
- php 
---
I have more "OMG, why didn't I know about this sooner!?" moments than I care to admit. In the past week, I've had yet another.

Blogs, talks, podcasts... these days you just can't escape all the hubbub concerning REST and RESTful applications. So, like any good lemming, I caved and gave it a shot. I created a practice application in Github using the Slim framework for PHP, and started coding.

OMG, why didn't I know about this sooner!?

Its a beautiful thing: RESTful development. It forces you to think in terms of resources and actions performed against them. It forces you to think about separation of duties, namely back end of front end. Most importantly, it teaches you that there's a whole world beyond GET and POST. Don't believe me? [See for yourself.](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)

The most impactful part to me was the separation of duties. I made some back end request routes that output JSON. I ran them manually in the browser to test them (no front end required). (Granted, I could have written tests for these, but since these are actual routes and not your "typical" class methods and function, that would require something like BDD and Behat, which I haven't quite grasped/mastered yet.) I was able to see that, at least for my GET routes, when I passed in certain parameters, I got expected (or sometimes unexpected) results.

Once I had that working-ish, I was able to write a single, simple HTML page as well as some javascript to make ajax calls (via dojo's xhr) to the PHP routes I had made, and display information on the HTML page via DOM manipulation. All this while realizing I could have just as well written a mobile interface in Objective-C, a command-line interface in LISP, or anything else! The front end is *truly* separate from the back end.

Like I said, it's a beautiful thing. My eyes have been opened and my life has changed. Am I going to start using RESTful development for all of my projects immediately? Nope. It has its uses, and I will appropriately use REST as needed. However, just the experience of playing with it and learning has really made me grow as a developer, almost overnight. I am both excited about and thankful for that.
