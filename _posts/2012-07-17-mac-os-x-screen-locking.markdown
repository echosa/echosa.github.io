---
layout: post
title: "Mac OS X Screen Locking Made Easy"
date: 2012-07-17 11:49
comments: true
tags: 
- mac
---
In "why the hell isn't the more known or documented better" news, a coworker of mine discovered and shared with me a neat little trick for locking Mac OS X: Control-Shift-Eject.

Mind you, this will only work if you are using an actual Apple keyboard with an eject key. However, prior to this, the screen locking solutions I found were as follows:

* have the screen saver turn on, possibly via a hot corner or hot key that I'd have to manual set
* choose 'Lock Screen' from the menulet that you can enable via Keychain Access -> Preferences -> General -> Show keychain status in menu bar
* write a custom applescript or Automator app/service to lock the screen, then set that to a key binding (per bullet point 1, above)
* Do a fast logout by clicking on the user switching menulet (if it is turned on in System Preferences) and selecting "Login Window"

Each of these either is a hassle or has unwanted side-effects that I didn't like. For instance, the fast logout option wasn't so bad, except instead of being left at a lock screen, it leaves you at a login screen, which means two things:

1. you have to select your account before entering your password (two step process, explained below), and 
2. other people have the option to login (not a *huge* deal, but not really desired by me at this point, and yes there are other accounts on my system).

The biggest of these two, for me, was number 1. When the screen is *locked*, all I have to do is press any key to "wake up", then type my password. That's not the case when you're at a login screen, of course. Having to use the mouse or keyboard to first select my user, *then* be prompted for my password became a hassle.

I'm not sure if this was added in Lion or previous versions of OS X, but I'm certainly glad to know it exists. So much so, in fact, I decided I should share this knowledge with the world. I know it doesn't particularly pertain to development, but I wanted to record it somewhere, if for no other reason than to have a resource where I can go back and remember "what was the locking key command?" in case I forget in the future.

So, yeah. There you go. Enjoy.
