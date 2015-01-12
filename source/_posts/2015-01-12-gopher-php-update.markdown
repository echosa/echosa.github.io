---
layout: post
title: "gopher-php and Phlog Update"
date: 2015-01-12 14:37:53 -0600
comments: true
categories: 
- php
- gopher
---
I recently updated my [gopher-php](https://github.com/echosa/gopher-php) package on GitHub as well as the [web interface to my phlog](http://echosa.freeshell.org/) that uses it.
<!--more-->
Most of the updates came about due to a change in the Gopher server that is serving my gopherspace. We are now using [Gophernicus](http://gopherproxy.meulie.net/gophernicus.org/) which supports some extra gophermap file types, most notably `h` for HTTP URLs.

Gophernicus brought with it some other changes as well, some of which required changes to not only the gopher-php library but my web frontend as well. While I was in there tinkering away anyway, I decided to finally get some items from my TODO list taken care of. Most notably, I added pagination as well as information about viewing the phlog via Gopher instead of HTTP.

Of course, the most interesting changes came in the form of updating the library and its unit tests. To my gleeful surprise, adding support for new gophermap item types (`h` and `i`, specifically) was as simple as updating a single switch statement; the rest of the library continued working and supported the new item types with no other changes. I should probably do something about that switch statement before it gets too unwieldy, though.

Anyway, it was nice to get some dev time in on this project. I do so much programming for other people and businesses and tend to spend my personal dev time on hobby projects. I'm glad I was able to work on something that is personal but also practical and in production, instead of just a hobby project.
