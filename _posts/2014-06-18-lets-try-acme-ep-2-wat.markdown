---
title: "Let's Try Acme: Ep. 2 - Wat"
date: 2014-06-18 09:17
tags: 
- acme
---
Now that [I've got Acme running](/blog/2014/06/18/lets-try-acme-ep-1-hello/), it's time to start giving it a fair shot.
<!--more-->
The first thing I notice is the color scheme. Not bad, but not changeable either. Makes me wonder what code syntax highlighting will look like.

...

Ah. No syntax highlighting, either. Well, ok then. I suppose I don't *need* syntax highlighting.

Welp, let's try typing some text. I open up a couple of editor windows, click in one of them, then move my mouse out of the way to start typing. I don't see any text. Scratching my head, I try typing some more text. Something catches my eye.

Huh. There's the text I typed. In a different window. Baffled for a bit, I click in the original window I was trying to type in again (maybe my first click didn't focus the window properly?), move the mouse out of the way again, and type some text. Again, I see no text in my window. I don't see text in the previously accidentally typed in window, either. A quick glance shows my text in yet another window.

Now I'm confused for a while, until I realize what's going on. Acme has mouse follow focus. The window that has focus is the one that the mouse is actually hovering over. When I moved my mouse of the way, I refocused Acme's cursor. Not what I was expected at all, and certainly not preferable.

Oh well. At least I figured that one out. I move the mouse over the still empty window I've been trying to type into this whole time. I type some some text and, hey, look at that! The text I typed is in the correct window!

I gleefully type some more text, pleased with my own achievement, all the while envisioning an Xbox style "achievement unlocked" screen. Now, let's try to save the file.

I know from my research that I need to middle-click `Put` to save. However, there's no `Put` tag for this window. That's simple enough to fix, I presume. Using the knowledge I have from my research, I simply type "Put" into the tags area for this window (making sure the mouse is over the tags area so it stays focused) and middle-click it. Certainly, since I'm trying to save a file that hasn't been saved before, it'll ask me where I want to save the file and what to name it.

Nope.

In fact, nothing happens. Nothing at all. I try middle-clicking a few more times to make sure I didn't do something wrong. Still nothing. After thinking about it for a while, I open an existing file to see how it works. Interestingly enough, it also does not have "Put" in its tag area. I type some text into it (ok, this mouse focus thing isn't so bad, except for the mouse cursor visibly being in the way sometimes), and notice that I then get the Put option. Ok, cool. You only see "Put" if there are unsaved changes.

Why am I not seeing "Put" in my other window, though? I gaze it at with all my staring power (learned from being a programmer for years) noting the differences. Ah. I see that there are several file related tags not present in my window that are present in the existing file's window. Obviously, this window isn't being considered a file window yet. The only other difference I see is that the first part of the tags area for the existing file is the file path. 

Let's fix that. I type a file path into the left side of the tag area of my new window. Hey! I have `Put` now! I middle-click it, and voila! The file is saved!

Achievement unlocked.

It then dawns on me that having to manually type the a new file name every time is going to be inefficient at worst and annoying at best. A little Internet searching leads me to a partial solution (really, more of a helper). `Ctrl-f` will do completion, so I at least don't have to type the entire file path out by hand. Not the best solution, but better than *not* having completion.

Speaking of completion, I wonder if I can complete text in my windows? I go to a window, type a word, then starting typing the same word and press `Ctrl-f`. Nope. It tries to complete file names only. That's a shame. If there's a way to do text completion, I haven't found it.

I decide to try one last thing before ending this Acme session. Coming from using Emacs and Vim, cursor movement is an important factor in my text editing. Obviously, Acme is mouse based, but certainly some basic cursor movement can be done with the keyboard.

I press the left and right arrows, and they work normally. I press the up and down arrows, and they scroll the window. Hm. I try a couple of other ways to move up and down between lines of text with the keyboard, including Emacs' `Ctrl-n` and `Ctrl-p` to no avail. As far as I can tell, you *have* to use the mouse to move the cursor between different lines. I understand that Acme (and Plan9) are very mouse-heavy, but this just seems ridiculous. Hopefully, I'm just missing something as the Acme noob I am. Either way, this whole using the mouse thing is new (especially having to use it this much), so there's going to have to be some concession on my part. We'll see how long it takes me to adjust, if I even can.
<hr />
A couple of side notes. This entire time I'm having to use an actually three button mouse. I attempted simply using my Mac's trackpad, but it has some issues with things like middle-clicking. Specifically, middle-clicking and *holding* the click down, especially when tapping instead of actually clicking (which I prefer, as I exclusively use tapping in my everyday work). I tried [BetterTouchTool](http://www.bettertouchtool.net), and it helped with clicking, but not with tapping and holding.

Also, for those who don't get the "Wat" reference in the title, [watch this](https://www.destroyallsoftware.com/talks/wat) (it's less than 5 min log).

In the [next post](/blog/2014/06/19/lets-try-acme-ep-3-problem-solving/), I discuss how many of my issues were resolved. You can read the previous post [here](/blog/2014/06/18/lets-try-acme-ep-1-hello/).
