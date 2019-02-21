---
layout: post
title: "linum-mode graphical glitch fix/workaround"
date: 2012-07-17T09:46:00-07:00
comments: true
tags:
- emacs
---
So, if you use graphical emacs on Mac OS X and you also use linum-mode (to show the line numbers in the left part of a window), you have probably noticed that there is a bit of a graphical glitch. To see what I'm talking about, look at the image that is linked [here](http://i.imgur.com/mt28I.png). There is [some discussion](http://emacswiki.org/emacs/LineNumbers#toc5) on EmacsWiki, but I didn't find an appropriate solution for myself.
<!--more-->
The issue is with a discrepancy between the left fringe and the linum-mode display. I guess the fringe puts a small border around itself, which overlaps the linum-mode display, creating the glitch. Since the fringe stuff is in the C source, its not easily or dynamically fixable.

That didn't stop me from figuring out my own solution, however. In reading the EmacsWiki notes, people suggested making changes to `linum-format`, which is customizable. Already that sounds good to me. However, there were a few issues with the solutions people posted. Either you had to set a static width (which I didn't want), or do some things that removed the right-justification (which I want) and the extra space between the line numbers and the buffer text (which I also want).

So, the first step was to get rid of the glitch. The best way I could come up with was to simply get rid of the left side fringe by using M-x fringe-mode and setting it to right-only. This removes the offending fringe on the left side, but leaves the right fringe, which is used for notification of wrapped lines, for instance. If you actually make use of the left fringe, obviously this part is not a solution for you, but it works for me (for now, anyway).

Then I had to get my line numbers displaying the way I wanted them to. The aforementioned `linum-format` can take a function as its value, so I came up with the following function:

```cl
(lambda (line)
  (propertize
   (format (concat "%"
                   (number-to-string
                    (length (number-to-string
                             (line-number-at-pos (point-max)))))
                   "d ")
           line)
   'face 'linum))
```

Put simply, this function finds out how many lines there are in the buffer, then uses that display the current line number, meeting the following criteria:

* The face is set the same as the normal fringe face (which, in my case, happens to be the default for the `linum` face). Without the call to properties, the line numbers take on whatever face that particular line has, which makes them inconsistent and distracting.
* All the displayed line numbers have the same width. This is important, because its easy to get linum-mode to shrink to the size of the line number, meaning line 1 will end up being longer than, for instance, like 1000, because the line number display will be wider at line 1000 than line 1.
* The line numbers are right justified.
* There is an extra space between the line numbers and the buffer text *that is the same face as the line numbers*. There are other solutions out there to get the extra space, but all the ones I tried had the extra space the same face as the buffer, which I didn't like at all. In fact, the only difference really between setting `linum-format` to my function, and setting it to dynamic is this extra space.

As I said, the only reason this works for me is because I'm ok not having a fringe on the left side. If you must have that fringe, you can still use the function above to format your line numbers, but you'll still have the graphical glitch.

Also, its worth noting that I made the function anonymous (a lambda function) because I have that function directly inserted into the customize value for `linum-format`. You could just as easily define that function with a defun in your .emacs or some other file, then set the function name (whatever you call it) as the value for `linum-format`.
