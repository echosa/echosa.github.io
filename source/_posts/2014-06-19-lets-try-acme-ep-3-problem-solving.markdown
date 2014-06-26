---
layout: post
title: "Let's Try Acme: Ep. 3 - Problem Solving"
date: 2014-06-19 17:26
comments: true
categories: 
- acme
---
The last few posts have shown some issues and complaints I've had with Acme so far. Surprisingly, these issues have quickly begun dissipating.
<!--more-->
First things first. If I'm going to be using `win`, I had to take care of the issues with prompt colors. `win` doesn't play nicely with the ansi color codes my bash prompt uses. This was an easy enough fix. I simply added a condition in `.profile` to only use color codes when I'm not in Acme (or in a Plan9 environment/application, really). 

Problem solved.

Next, the big issue. Mouse vs trackpad clicking vs trackpad tapping. As I've stated before, I'm very much a tap guy. Luckily, I came across [this video](http://research.swtch.com/acme), which anyone considering or wondering about Acme should be required to watch. Anyway, looking through the comments, I learned that when using my MacBook's trackpad, if I hold down Option and tap (or click), it sends a middle click to Acme. If I hold down Command, it sends a right click, as usual. 

"But what about chording?", you might be asking yourself. Well, I have three finger drag turned on. The interesting thing about three finger drag is that you don't actually have to drag with with all three fingers. You can simply place three fingers down and drag with just your index finger, just as you would move a mouse - including being able to pick your finger up and down to continue moving in the same direction. So, effectively, this becomes a single left-click drag. 

The end result? I can put three fingers down, drag with my index finger to select some text, then while still keeping my fingers down, press Option to cause a middle click (which cuts the text), then press Command to cause a right click (which pastes the text). I can then move the cursor somewhere else, put three fingers down and press Command to paste again. Touchpad tap chording!

Problem solved. 

Though to be fair, I haven't gotten holding down button two then pressing button one to work yet. Then again, I haven't needed it yet, either.

Moving on, I decided to try and edit some code. The first glaring issue with Acme was the default font. I prefer, nay, *need* a monospaced font when coding. The default Acme font didn't cut it. Luckily, the font is one of the few things that Acme lets you easily customize. Just add a `-f` option, like this:

```
9 acme -a -f /usr/local/Cellar/plan9port/20140306/libexec/font/fixed/unicode.9x18.font &
```

Remember, the plan9port for OS X makes it such that you run plan9 commands through the `9` wrapper command. Also, I added the & to my Acme command so that it doesn't hijack a whole terminal that has to stay open.

Problem solved.

Now that I had a monospaced font, code was easier to work with. However, I missed the ability to do things like `ci"` in Vi(m). What that does is delete all text in between the surrounding double quotes so you can replace the text. Well, Acme has its own version. Simply double-click just after the opening quote (or just before the closing quote) so select all text inside. This also works with parentheses, braces, etc. Nice.

Problem solved.

With all these solutions, Acme has become more than usable for me. To be fair, though, there are a remaining number of issues, complaints, and hangups I still have.

The lack of colors, especially syntax highlighting, is still up in the air as to whether it is an issue or not. We'll see what time will tell.

The mouse focusing windows simply by moving over them still trips me up. It's great when I remember it and use it. It's not so great when I forget, move my mouse cursor out of the way (due to habit), then start typing only to have the text inserted in the wrong window. This will just take some getting used to.

`win` comes through as just a dumb terminal, so not everything works. For instance, `git diff`. I can get by with just using my regular terminal instead. That's what I normally do, anyway, when I'm not using magit inside Emacs.

I'm starting to see why some people keep a file around with tags they commonly use. It would appear that, while I can add my own tags to the tag bar, they are not persistent. I have to add them again everytime I close and open Acme.

Speaking of files, file navigation is still a bit clunky. Right-clicking down a long directory tree is cumbersome (especially having to find the right directory to click on in each window), and leaves lots of unwanted and unnecessary windows around until I manually delete them. The only other option I see is to use the file name part of the tag bar (all the way to the left) to type in a full path. Luckily, the `Ctrl-f` completion makes this faster.

Still, even with all this, Acme is, at this point, a completely useable and worthwhile editor for me. I look forward to using it more and learning more about it. 

This post was written in Acme.

In [the next post](/blog/2014/06/26/lets-try-acme-ep-4-enough-messing-around/), I finally get down to writting some code.
You can read the previous post [here](/blog/2014/06/18/lets-try-acme-ep-2-wat/).