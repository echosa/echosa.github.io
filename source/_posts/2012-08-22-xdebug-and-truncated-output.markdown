---
layout: post
title: "XDebug and Truncated Output"
date: 2012-08-22 08:42
comments: true
categories: 
- php
- xdebug
- zendframework
- zf
---
Having used Zend_Debug::dump() with XDebug for quite some time, I've finally gotten tired of seeing truncated output. What I mean is, when I have Zend_Debug::dump() display a stack trace (for instance), it will show the first few lines then truncate with and ellipsis. This is fairly useless. Sure, I *could* go to the error log, but there's a reason I'm dumping this to the screen (when I'm in developer mode and have the show debug info flag for my application turned on... don't worry, this doesn't happen in production). For a while now I've just put up with it, thinking it an issue with Zend_Debug. 
<!--more-->
I was wrong.

Its actually an issue with XDebug and the amount of information it will show. Even just using var_dump by itself (Zend_Debug uses it internally) will result in truncation. However, this is a one line fix. In your php.ini, put this:
    xdebug.var_display_max_data = -1
or in your application config, you can set this at run time like this:
    phpSettings.xdebug.var_display_max_data = -1
The -1 tells XDebug to display an infinite amount of data. No more truncation!

You might ask why I'm Zend_Debug::dump()-ing my stack traces anyway, instead of just printing or echoing them. Well, because SHUT UP THAT'S WHY. Seriously, though, its just something I've done since I started using Zend Framework that has stuck around with me. I'm only human, which is slightly better than [almost human](http://www.youtube.com/watch?v=zQTimBTkYzw).