---
layout: post
title: "Let's Try Acme: Ep. 5 - Well, Shit"
date: 2014-06-27 16:17
comments: true
categories: 
- acme
---
Well, shit. I made my first huge Acme mistake, and I paid the price.
<!--more-->
Long story short: Acme has its own `rm` command. I don't know exactly how, but it works differently than the one I'm used to. Some combination of that and how Acme executes commands screwed me.

Big time.

I tried to delete some obsolete directories in my home folder. In the directory listing window for my home folder in Acme, I found the thing I wanted to delete (in this case several things), and added and `rm -Rf` before it and an asterisk after it, like this:

```
# other files here
rm -Rf .offlineimap*
.offlineimap.py
.offlineimap/
# even more files here
```

As you can see, along with the other things in my home directory, I had several offlineimap related things. I wanted to delete them, and `rm -Rf .offlineimap*` is how I would normally achieve this. 

My first clue that something was wrong should have been when I got an error that `-R` wasn't a proper flag. `-r` was required instead. Hm. I could have sworn that `rm` took a capital R, but I tend to get capital and lower-case R confused in various commands, so I just went with it. I changed the R to an r and executed the command. After running `Get` to see the updated contents of my home folder, I realized that a *lot* more was missing than just the offlineimap stuff.

In fact, *most* of my home folder was gone. Luckily, I had a backup from just a few nights ago, so I was able to restore with minimum loss. However, this is a mistake I won't be making again.

Also, always keep backups.

This post was carefully written in Acme.

In the [next post](/blog/2014/07/07/lets-try-acme-episode-6-trouble-in-paradise/), I break down and go back to Emacs for a night. You can read the previous post [here](/blog/2014/06/26/lets-try-acme-ep-4-enough-messing-around/).