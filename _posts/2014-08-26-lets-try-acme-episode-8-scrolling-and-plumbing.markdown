---
title: "Let's Try Acme: Episode 8 - Scrolling and Plumbing"
date: 2014-08-26
categories: [blog]
tags: 
- acme
---
After using Acme for over two months now, I finally figured out two fairly basic things: scrolling and plumbing.
<!--more-->
Let's start with scrolling. I knew (and have explained before) how scrolling works by scrolling down with right-click, scrolling up with left-click, and scrolling to an exact position with middle-click. I've also explained how the amount scrolled is directly tied to where the mouse cursor is in the scroll bar. If the mouse is pointing close to the top of the scroll bar, you'll scroll a little amount. If you're pointing at the bottom of the scroll bar, you'll scroll a lot, up to a full page.

What I've recently learned is that these "little" and "lot" amounts are not arbitrary. Where you point is exactly the line that will be used to scroll to. So, if you point to the scroll bar next to line 10 and then right-click, you'll scroll up such that line 10 is at the top of the window. If you then left-click, you'll scroll down so that line 10 is back where is was (on the line the mouse is pointing to). So, scrolling down puts the line your mouse cursor is on at the top of the window, while scrolling up puts the line at the top of the window where the line you're mouse cursor is pointing to is. This allows for some really specific scrolling and is quite useful in that regard.

Let's move on to the next thing I figured out: plumbing. This is really more of a plan9port thing (or, more generically, a Plan 9 thing), but it ties directly into Acme. The plumber in Plan 9 is essentially a program or process that allows for routing of requests to determine actions to take. It's similar to the `open` command in OS X. 

As far as Acme is concerned, the plumber is what allows different things to happen when you right-click different bits of text. For instance, right-click a file name to open a file. Right-click a directory to open that directory. Right-click a URL to open it in your web browser. You, as a user, are just right-clicking on text, and that text is sent to the plumber to determine the action to take.

The great thing is that you can add your own rules to the plumber! I've seen where people have added rules that allow them to, for instance, right-click `GH1234` and be taken to GitHub issue #1234 in some project. I, however, used the plumber to make my life in one particular project significantly better.

I have a project I work on that lives in a VM, but the dev work is all done on the host machine. So, on my host machine, I have a directory called `/mnt/project1`. This directory is the project root and has all the code in it. However, this directory is mounted in the project's VM as `/www/sites/www.project1.com`. The way this project works is that all tests are run in the VM. This means that when I get output (in Acme, of course, because I'm running my tests in an Acme win session), the errors I see are rooted in `/www/sites/www.project1.com`. That's not where the files are on my host, though, so right-clicking the files in the errors does nothing. 

At least, it *did* nothing until I added a plumbing rule to recognize `/www/sites/www.project1.com` and replace it with `/mnt/project1`. Now I can right-click these files in the errors and stack traces and be taken directly to the offending line in the file. If you're curious what that plumbing rule looks like, here it is:

```
# project1.com rules

project1RemotePrefix='/www/sites/www\.project1\.com/'
project1LocalPrefix='/mnt/project1'

# /www/sites/www.project1.com -> /mnt/project1 (with "on line" number)
type is text
data matches $project1RemotePrefix'(.+) on line ([0-9]+)'
arg isfile $project1LocalPrefix/$1
data set $file
attr add addr=$2
plumb to edit
plumb client $editor

# /www/sites/www.project1.com -> /mnt/project1 (with line number)
type is text
data matches $project1RemotePrefix'(.+):([0-9]+)'
arg isfile $project1LocalPrefix/$1
data set $file
attr add addr=$2
plumb to edit
plumb client $editor

# /www/sites/www.project1.com -> /mnt/project1 (without line number)
type is text
data matches $project1RemotePrefix'(.+)'
arg isfile $project1LocalPrefix/$1
data set $file
plumb to edit
plumb client $editor

```

As you can see, I actually have three rules, one each to match the following file/line output strings, respectively:

```
# file with line and column numbers
/www/sites/www.project1.com/src/path/to/file:10:8

# file with line number
/www/sites/www.project1.com/src/path/to/file:10

# just the file name
/www/sites/www.project1.com/src/path/to/file
```

I might be able to improve or combine these rules, but this is how I was able to get it working, and if it ain't broke I'm not fixing it.

So, you can see how the plumber can be quite useful. It has certainly helped me, and I will definitely be making more rules as the need arises. 

The next episode of "Let's Try Acme" might be a bit different. Now that I've used Acme for over two months straight, I'm considering going back to Emacs to see how it feels, what I miss, what I enjoy, and really allow myself to compare and contrast the two different workflows. Then again, I might not, so I make no promises. You can read the previous post [here](/blog/2014/08/07/lets-try-acme-episode-7-equilibrium/).

Edit: The [next episode](/blog/2014/10/06/lets-try-acme-episode-9-the-end/) is the end of the road. (For now?)
