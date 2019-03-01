---
title: "New GOPHER Library for PHP"
date: 2014-02-25
tags: 
- php
- gopher
---
Well, I've gone and done it. I've created a library for reading and parsing [GOPHER](http://en.wikipedia.org/wiki/Gopher_(protocol%29) files from PHP.
<!--more-->

I've recently been playing with GOPHER again, and it's been a great blast from the past. I even started a phlog (a GOPHER blog, basically). However, I realized that not everyone is awesome enough to use GOPHER, so I wanted to make my new phlog available via HTTP as well. Enter gopher-php.

You can find the library [here on GitHub](https://github.com/echosa/gopher-php). It is quite tailor-made for my own usage, so it is pretty incomplete in terms of GOPHER features and support.

To see it in action, you can check out [my phlog's http web frontend](http://echosa.freeshell.org). In comparision, you can see my phlog via the GOPHER protocol by either visiting [this link](gopher://sdf.org/1/users/echosa/phlog) using a GOPHER client ([lynx](http://en.wikipedia.org/wiki/Lynx_(web_browser%29) recommended) or by using a GOPHER web interface such as [this one](http://gopherproxy.meulie.net/sdf.org/1/users/echosa/phlog) (link will take you to the phlog).
