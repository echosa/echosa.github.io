---
title: "CTRL-less emacs? (Or, at least, less CTRL...)"
date: 2012-03-21
tags:
- emacs
---
Things I love about emacs:

* (E)LISP and the ease with which extensions, modes, functions, etc. can be developed
* Buffer/frame support
* M-x customize
* Mark/point, registers, kill-ring
* It does everything*
* The power. My God, the power.

This is not a complete list, but it goes to show that emacs is great and I love it for reasons. However, especially as of lately, I've been experiencing the beginnings of emacs pinky. You know what I'm talking about. Holding down the ctrl button for significant amounts of time has been leading to the side/pad of my left pinky being sore and uncomfortable, even with using Caps Lock as my control key. (It's *way* worse when I have to use the real control key.)

This is something I want to fix.
<!--more-->
I should probably mention why I'm holding down ctrl so much. I'm a PHP developer. Lately, I've been doing a lot of editing/refactoring. This means I spend quite a bit of time moving around the buffer. I don't use arrow keys, I use ctrl-n, -p, -f, and -b (as well as their M- versions). I also use registers and other handy emacs functions. The following hypothetical key stroke sequence is not much different form real usage for me:

```
C-a C-space C-n C-n C-n C-x r s o C-s C-s C-s C-s C-k C-x r i o C-n C-n C-n C-k C-n C-y C-s C-s C-s C-x r i o
```

That's a lot of holding down control, especially when I'm doing this sort of editing for literally *hours*. Its no wonder my pinky gets sore. I have been making use of macros (C-x ( ) lately, and that helps a *bit*, but still, I end up in situations like the above. Therefore, I've been trying to think of/discover ways to alleviate my pinky of its ctrl-prison. Here are some of the things I've come up with:

* Use arrow keys (I'd really like to stay on the home row)
* Use the mouse (Good God, no)
* Use searching to get around instead of line/column movement. This is fine if I need to reach something much further up or down in a buffer, but not when I want to work on consecutive lines. Then its much easier/faster to use line/column movement instead of searching to get where I need to be.
* Use something like viper-mode (or the more recent evil-mode) to give me VI(m) like capabilities. This is honestly something I've been off and on about using for a while, and I've tried viper a time or two. I'm really considering this again.
* Use control-lock. I've done this before, but its not as good as it seems (in my experience). Control-lock is a mode which does exactly what the name implies, it "locks" ctrl as "on" similar to Caps Lock for shift. That way, you can toggle control-lock on, then just type n, n, n, n, k, n, y to move down four lines, kill the line, move down again, then yank your kill. Its a really good idea, and has proven useful before, but I just couldn't get used to use it for long stretches of editing like my example above. It just didn't feel right, and sometimes got a bit confusing (though the latter is probably more my own fault).
* Find a way to map searching (C-s) the same way that running macros (C-x e) are mapped. That is, with macros, you press C-x e to run the macro, then just press e to run it again and again, whereas with searching, you have to keep pressing C-s to repeat the search.

I've had some other fleeting ideas, but can't remember them at the moment. If you have any tips or suggestions for use emacs with less CTRL, please comment and let me know. For now, I think I may have to try a VI(m) hybrid mode (again).
