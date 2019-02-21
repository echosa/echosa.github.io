---
layout: post
title: "Listing all key commands for a given prefix"
date: 2012-07-26T06:45:00-07:00
comments: true
tags:
- emacs
---
So, when it comes to register/bookmark/rectangle/etc commands, I tend to forget which keys run which commands. They all use `C-x r` as a prefix, which makes it all the more easily forgettable. Luckily, emacs is (as always) one step ahead of me. Typing `C-h` after a prefix will show you all bound keys/functions for that prefix. So, typing `C-x r C-h` shows me all the `C-x r` keybindings available and what they do.
