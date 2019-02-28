---
title: "Let's Try Acme: Ep. 4 - Enough Messing Around"
date: 2014-06-26 15:27
tags: 
- acme
---
This is it, folks. It's time to finally roll up my sleeves and do some programming in Acme.
<!--more-->
I'll get this out of the way right off the bat. *So far*, I haven't missed syntax highlighting. Strange as that may sound, it's true. Time will tell on whether or not lack of colors becomes an issue, but for now it isn't. 

With that out of the way, a little background. I decided to use a small PHP/Symfony2/Angular.js app as my first foray into coding in Acme. That means I don't need to compile, but I already had a Makefile written that runs various checks and test on the code. Also, this application is already a git repo. Coming from Emacs, and having read about Acme being an "integrating editor" that integrates with your existing system and lets you run things and use tools you already have on your system, I decided I should be able to work with make and git from Acme.

Long story short: both were large successes. 

Since I hadn't touched this code in a while, my first steps were to check to see if git was clean (make sure I didn't have any uncommitted changes hanging around from before) and to make sure my application still passed all its tests. I decided to start with the latter. Since commands in Acme run in the context of the window in which they are run, I needed to get to my project directory to run make. 

First, I simply opened a `win` window, changed to my project directory, and ran make from there. So far so good, but did I really need a shell window open for this? Certainly not. I closed the window, and navigated to my project root in the directory listing window(s). I knew it was only a couple of directories away from the starting directory window Acme gives me every time I open it, otherwise I would have simply opened a new window, typed in the directory, and used `Get`. 

Anyway, now that I had a directory window open to my project's root, I simply typed `make` into the tag bar and middle-clicked. The Makefile ran perfectly, and showed me that I had some outstanding issues. Part of the output of make, of course, was the file name of the offending file. Could it be so easy? I right-clicked the file, and it opened in a new window. Awesome. That'll certainly save time.

I fixed the issue, and ran `make` again. Everything passed. Awesome. Now, let's go see what my git status is like. Next to `make` in the project directory window's tag bar, I add `git status`. Since there's more than one word in this command, I know I need to highlight it to run it. Luckily, I remember that simply pressing `Esc` will select the most previously written text. I do so, `git status` is highlighted, and I middle-click. Git runs as expected, and the output is appended to the same window as the `make` results. I thought this would be an issue, but it actually never hindered me the entire time.

Inspecting my git results, I see that there was a file modified that hadn't been previously committed. I couldn't remember what was in that file, so I needed to run `git diff` on it. Since Acme is just text, I actually typed "git diff " before the file name right there in the git output, selected and right-clicked (I'm working with a scroll wheel for a third button, so middle-button dragging is a pain), and the diff was run and the output once again appended to this window. Very convenient being able to turn the previous output into my next command quite easily.

I see the diff and remember what I had done. A couple of minor changes that just hadn't been committed yet. Well, may as well commit it now. I made a `git commit -am "some message"` command in the tag bar, but unfortunately it actually didn't work. Sadly, I don't recall the issue right now (I really should have taken notes), but it was easy enough to circumvent this by simply opening a `win` window to run the commit. I could have just as easily switched to regular terminal, but again, the goal was to try and work in Acme. I'm still investigating the `git commit` issue, though. I haven't given up on that yet.

Now that I knew I could run my tests and use git, it was time to actually do some coding. I checked my TODO list for the app, and chose a task. Opening the first file I needed was pretty easy, though the whole right-click to navigate directory windows is still a little cumbersome at times (mostly, its finding the right directory or file to click on each time that's the issue). I knew the function I needed to get to as a starting point, so I typed part of its name in the tag bar and right-clicked to search and get to it in the code. This as it turns out, became a very important and useful part of navigating code.

I made some changes in the code and ran `make` again. Easy. As a bonus, everything still passed. Rinse and repeat, throwing in a few git commits for good measure. Honestly, the only trip ups I really had were when I tried to use the keyboard for navigation (those up and down arrows still get me).

The end results is that the programming session went well, Acme stayed out of my way but was also there when I needed it to be, and all the tags and mouse clicks and other stuff that make Acme what it is quickly started becoming natural and intuitive.

I like Acme, y'all. I can admit that now. I'm not ready to call it my editor of choice, but I like it. It's neat. It's quirky. It's fun. Most importantly, it's useful.

One final thing I want to mention. Due to Acme's interestingly limited take on the whole tabs/spaces/indenting thing, I did end up having to write my own indention commands. However, they were staggeringly easy. I have started my own Acme commands file, where I can keep a tool set of useful commands. For instance, I wrote this to get rid of trailing spaces:

```
Edit , s, *$,,g
```

However, because of the way this command is written, it has to be run from either the window you want to affect or it's tag line. That means copy/pasting (or rewriting) it every time. I eventually found a stop-gap solution, which let's me specify a regular expression which will run the command in all windows that match. Since I was working in PHP, I wrote this to remove trailing white space in all open PHP windows:

```
Edit X/\.php$/ s, *$,,g
```

Still not satisfied, I delved deeper into the capabilities of the 2-1 mouse chord. What this chord lets you do is select some text with the left mouse button, then select a command with the middle button, and, *while still holding the middle button down*, press the left button. This is called a 2-1 chord, because you're holding down button 2 (middle-click) and pressig button 1 (left-click).

The end result is that the text that was selected is passed as an argument to the command executed with 2-1. It's not as complicated as it sounds (or reads, in this case). For example, I can put this in the tag line for a window in which I want to perform an edit command:

```
Edit
```

and then have this command text anywhere (like my Acme commands file or even this very file):

```
s/ *$//g
```

Then, I can select the command text and, with it selected, perform a 2-1 chord by middle-click holding then left-clicking Edit. It's a lot to type, but it's actually quite awesome and pretty ingenious. This whole mouse chording thing has opened my eyes to new ways to use Acme. 

Addendum (July 9, 2015): Having been using Acme as my primary editor for a while, I have to say it is almost imperitive to get a mouse with a real middle button. I recently broke down and finally bought an [Evoluent mouse](http://evoluent.com) to try. It's nice, although quite different. However, having a three-button mouse makes 2-1 chords way easier and faster to perform.

Additionally, if you want to be able to 2-1 on a MacBook, [this blog post](http://www.mostlymaths.net/2013/04/just-as-mario-using-plan9-plumber.html) has a patch you can apply to the plan9port source file and recompile. Look for it towards the end of the post, just above "Final Remarks".

This post was written in Acme.

In the [next episode](/blog/2014/06/27/lets-try-acme-ep-5-well/), I discuss my first big mistake in Acme and the price I paid. You can read the previous post [here](/blog/2014/06/19/lets-try-acme-ep-3-problem-solving/).
