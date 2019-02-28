---
layout: single
title: "Zork Fortress Update: 0.0.2"
date: 2015-03-29 15:56:04 -0500
comments: true
tags: 
- clojure
- zork-fortress
---
I recently released version 0.0.2 of my zork-fortress project, and by "released" I mean "added a new git tag".
<!--more-->
In spite of my lack of work on the project the past few months, it is far from dead! I finally got some time to work on it, so here's the list of 0.0.2 updates from the [CHANGELOG](https://github.com/echosa/zork-fortress/blob/0.0.2/CHANGELOG):

- Added the `help` command.
- Added the `chop` command.
- Added the `inventory` command.
- Reformatted `history` output.

I also did some code refactoring and got all [core.typed](http://typedclojure.org) static typing in place.

As is, when you run version 0.0.2 of the game, you can look around (you'll see a single tree until you chop it down), chop that tree down, check your inventory (it'll be empty until you chop the tree), get help for commands, and see your recent command history. It's not much, but it's a start.

I've got quite a few ideas for 0.0.3 and beyond, including some major changes to the chop command, so don't get too comfortable with how it works now.
