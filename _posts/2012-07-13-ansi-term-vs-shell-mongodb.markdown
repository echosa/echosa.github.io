---
title: "ansi-term vs shell: mongodb"
date: 2012-07-13
categories: [blog]
tags: [emacs]
---
So, I've been messing about with MongoDB lately. Its pretty cool. You start the server then run the `mongo` command, which takes you to a repl environment where you can run commands and try it out.
<!--more-->
In a typical terminal this works great. However, I tend to use ansi-term most of the time. I can run most things in ansi-term, including vi(m) and cli emacs (leading to emacseption). Mongo (as well as other things, like sftp, etc) has issues though. The backspace key doesn't exactly work as expected. Sure, its technically doing its job, but the output and buffer become messed up and its quite annoying.

A bit of searching around led me to the conclusion that I should try M-x shell instead. I've never used shell, eshell, or the like. Never really had a reason too; ansi-term has always been good enough or better. In fact, I thought that you couldn't run processes/programs in shell, but I was wrong. I ran M-x shell, then ran mongo and viola: it works!

Now I have even one less reason to leave emacs or have another program open. Added bonus: I get to use a part of emacs I previously never used! Time to learn how I can hack it to make it even better!
