---
layout: post
title: "I'm Slowly Getting ORGanized"
date: 2010-05-11T15:04:00-07:00
comments: true
categories:
- emacs
- org
---
I've found myself using ORG mode a LOT lately, mostly at work. I'm really come to like it, and it has basically because my todo list for work. Of all the useful features ORG has, there is one that I never learned about until recently: links. I'm sure I should have known about these long ago, but for some reason I didn't.
<!--more-->
Anyway, links are just what the name implies: clickable links to other places (though, the mouse is not necessary). This can be to a url, a file, or even a specific place in a file (i.e. line number, certain word, etc). I find this extremely useful as a programmer.

For example, I find a bug in a program. I place a TODO item in my org document to fix the bug. Inside the description, I can then place a link to the file where the code to be fixed is, or more specifically, I can link it to an exact function/method or even line number! Then, when I get around to that TODO item, I simply activate the link, and the file loads up, ready to fix!

There is one small caveat though. By default, org will open the file in a different window. Some might like this, but I have one main window in my emacs frame that is for working in (org files, source code, etc). So, when I've viewing my org document and activate a link, I want the file to load in that same window. A quick Google search revealed a simple fix for this: customize the variable `org-link-frame-setup` and change `file` to use the function `find-file` instead of `find-file-other-window`. Easy enough!
