---
layout: post
title: "Showing what makes a line too long"
date: 2012-07-31T07:31:00-07:00
comments: true
categories:
- emacs
---
I'm a programmer. In many ways, I'm a bit of an old-school programmer. For instance, I like my lines no longer than 80 characters. I found myself wanting a visual cue warning me when I go over that limit, and in my search for solutions I found a few options.
<!--more-->
The first option is make sure I code in a window that is exactly 80 characters wide. This is nice and easily done with Emacs using multi-windows frames or making sure your frame is the proper width. I usually (or at least, used to) do the former. However, this does require manually handling windows/frames/etc. which can be a pain at times.

The next option is to look at the various packages for handling long lines or column visualization and pick one. Some will put a long vertical bar at a given column, but in my experience the display will get messed up. There are many packages that are meant to help handle long lines, but I've yet to find one I really liked. Plus, why use an external package when Emacs already has what you need?

Which brings me to option the third. These days Emacs comes with whitespace-mode, which is an incredibly powerful and customizable tool. You can use it to show visual whitespace (show spaces, tabs, paragraph marks, etc), lines that are too long, blank lines, trailing whitespace, etc. In my case, with a couple of lines of code, it can be used to show you lines that are too long (lines over 80 characters).

In the hook for whichever mode you want this visualization/decoration, place the following lines of code:


```cl
(make-local-variable 'whitespace-style)
(setf whitespace-style '(face lines-tail tab-mark))
(whitespace-mode t)
```

What this does is make the variable `whitespace-style` buffer local (so that any customization or changes outside of the buffer won't affect how whitespace-style decorates the current buffer) then set the variable to a particular value. I have chosen the value '(face lines-tail tab-mark).

* "face" has to be there (and must be first, I believe) in order for anything to be visible. No matter what other settings you choose, if "face" isn't there you won't see anything.
* "lines-tail" will highlight any characters past the `fill-column` (mine is set to 80) on each line. This is an important difference from the "lines" option, which will highlight the entire line if it is longer than `fill-column`. I prefer to only have the offending characters highlighted so that I know where to break the line if necessary.
* I also set "tab-mark" because I don't use TABs; I only use spaces. If I open a file and it is using TABs, I want to know.

The third line turns on whitespace-mode so that the decorations will be rendered. You'll know that whitespace-mode is on if you see "ws" in the mode-line.

There are many more options that can be set for `whitespace-style`. You can see them all by looking at the help page with `C-h v whitespace-style`. Keep in mind that you'll need whitespace-mode loaded before you can view the help page.

I'm sure you could also turn on whitespace-mode globally. I wouldn't want that, however, so I just put those three lines of code in my mode hooks to enable it for each mode I want it in.
