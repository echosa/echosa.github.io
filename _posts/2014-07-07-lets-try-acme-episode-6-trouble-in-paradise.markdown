---
layout: single
title: "Let's Try Acme: Episode 6 - Trouble in Paradise"
date: 2014-07-07 09:08
comments: true
tags: 
- acme
---
So, there I was, doing some PHP work in Acme, when I broke down and went back to Emacs for the night.
<!--more-->
Honestly, there were two reasons for switching back: [Projectile](https://github.com/bbatsov/projectile) and buffer/window handling. 

Let's start with the latter. Acme is nice and all, but as you start getting more and more windows open, they become harder to manage. Worse still, you can't "hide" any windows, with the exception of being able to hide all but one in a column. This means that the more windows you open, the more you clutter your workspace. 

In contrast, Emacs hides all those buffers in the background, letting the user get back to them easily and quickly when needed, without them causing clutter. This was becoming a big issue in Acme to where I was having to close convenient windows just to declutter.

Now, to the big one: Projectile. The code base I was working in is large. Really large. Navigating around it in Acme was doable, but not convenient or quick. Finding files or greping text was also inconvenient, especially since Acme uses a plan9port version of grep (as well as other commands... see the [last post](/blog/2014/06/27/lets-try-acme-ep-5-well/) for my issues with rm), so I ended up needing to actually run /usr/bin/grep explicitly to get, in this case, recursive functionality. 

Projectile makes project navigation and finding what you need simple and fast. It automatically limits searches to the root project directory, allows you to do fuzzy or partial matching with live results, and just makes project navigation a breeze.

Sorry, Acme. Emacs wins this round. Then again, I typically limit my learning new editors to hobby projects, specifically *not* using the new editor for actual work. The fact that I was able to work for at least some period of time in Acme before switching is a testament to the good Acme has to offer.

If there's a Projectile-ish workflow for Acme that I'm missing, please let me know. There are probably some Acme commands I could write to do this; hell, I could probably write an Acme command to run Projectile *from* Emacs, and use its results. (Hm... I might have to try that.) Then again, maybe I'm just missing something in Acme. I doubt it, though, since Acme is fairly bare bones and meant to integrate with your existing environment (except when plan9port's binaries overshadow your system ones).

I haven't given up on Acme, yet. That time might be coming, but I'm trying to give it at least a month. Come on, Acme. You've wowed me once. It's time to wow me again.

This post written in Acme.

[Next time](/blog/2014/08/07/lets-try-acme-episode-7-equilibrium), things are significantly better.
You can read the previous post [here](/blog/2014/06/27/lets-try-acme-ep-5-well/).
