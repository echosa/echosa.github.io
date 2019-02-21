---
layout: post
title: "I Got This (key)Board On Lockdown"
date: 2009-06-30T20:23:00-07:00
comments: true
tags:
- emacs
---
The longer I use emacs, I find myself sticking to my keyboard's home row. Even in my pre-emacs days I was already starting to ignore my mouse, but these days if I can't do something without mostly remaining on "asdf" and "jkl;", I either find a way, create a way, or (rarely) learn to deal with it (and/or try to avoid it). That is not just for emacs either. Other programs, even my tiling window manager, are all used mostly by keyboard. As you can imagine, I've learned a lot of keyboard shortcuts.
<!--more-->
As a side note (but not a tangent, I promise!), one of the things I like about vi and vim (yeah, yeah, boo, hiss, etc.) is its use of h, j, k, and l for movement. (I don't like having to switch modes to do so, however, which requires leaving the home row to press escape [though I have read of techniques to set, for instance, 'jj' or 'jk' (typed really fast) to the same as escape for going from insert mode back to visual mode], but that's getting into tangent land, so I digress.) I like using these keys for movement because it allows me to stay on the home row and not have to move my hands to the arrow keys. While I have thought about what emacs would be like if its movement keybindings were closer to vi's (i.e. C-j instead of C-n for next-line), I've become quite accustomed to using emacs' defaults for moving around.

This, of course, sometimes requires extended and extensive holding down of the control key. This is also true when doing something like cutting/pasting lines and moving. For instance, to switch two lines of text, I have to go to the beginning of the first line then press: C-k, C-n, C-y. Of course, I don't actually press control three times, since I (improperly, I think) use only my left hand for control. I hold down control and press k, n, y, then release. While this small, three command example is no problem, sometimes I do major editing which requires holding down the control key for quite some time. This can be uncomfortable, problematic, and lead to the infamous [emacs pinky](http://en.wikipedia.org/wiki/Emacs#Emacs_Pinky), even if [using caps lock as a control key](http://www.emacswiki.org/emacs/MovingTheCtrlKey).

Certain that someone else has found this a hassle and done something about it, I looked around and found [control-lock](http://www.emacswiki.org/emacs/ControlLock). It works much like caps lock: you turn it on (with C-z) then all keys pressed are interpreted as if control is being pressed. So, instead of pressing C-n ten times to move down ten lines (I know, I know, prefix arguments and all that... this is just an example!), I can simply press C-z, then press (or hold down) n. Pressing z, which translates into C-z, exits control-lock.

I have to say, I have found control-lock extremely helpful mostly when editing a file. Typically, when I'm writing or coding, I don't do much that requires the control key except deleting a few characters and slight cursor movement. It's when I'm going back and editing that I use a lot of control commands back-to-back. That is where control-lock comes in very handy. It saves time, effort, and discomfort. I highly recommend it.
