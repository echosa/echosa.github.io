---
layout: single
title: "Node.js and TurnTable.fm"
date: 2013-04-12 14:40
comments: true
tags: 
- node
---
So, a friend recently turned me on to [TurnTable.fm](https://turntable.fm) which is an awesome place to listen to, discover, and share the music you love. In checking out some of the different rooms, I discovered that some people had written bots that do different things: manage who can play songs, post fun messages, keep stats, etc. Out of curiosity, I decided to try my hand at making a bot.
<!--more-->
I quickly found [an api for working with TurnTable.fm via Node.js](https://github.com/alaingilbert/Turntable-API). This set me on a path to try out and learn programming with Node.js.

My initial reaction? My God, the callbacks.

Basically everything is asynchronous so when you call a function, if something needs to happen when it's done, that "something" has to be passed in the form of  a function as an argument. Its definitely a different way of thinking about programming, mostly (for me anyway) because I struggled to find the end points. If I just keep calling callback after callback after callback where will it end? Eventually, and after quite a bit of programming in this way, I began to get a feel for it.

My current reaction? This is awesome. 

I really enjoy the experience of programming for Node.js and I'd recommend it to others. There are lots of packages, test utilities, and lots of cool stuff written in Node.js, and I can now understand why.

Feel free to checkout my code. It is [hosted on GitHub](https://github.com/echosa/ImproverBot). For now, I'm pretty much done working on it, but I may revisit it again in the future. Either way, it was a great learning experience that I very much enjoyed.
