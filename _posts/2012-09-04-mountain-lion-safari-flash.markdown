---
title: "Mountain Lion, Safari, and Flash"
date: 2012-09-04
tags: 
- mac
---
So, if you're like me and you upgraded to Mountain Lion (OSX 10.8) only to have Safari continuously tell you that Flash is a "blocked plugin" and is out-of-date (no matter how many times you update and install the latest), you're probably ready to rip your hair out (or use Chrome like a quitter). Well, here's how *I* fixed the issue. Hopefully this works for you, too.
<!--more-->
Either in Finder or Terminal go to `/Library/Internet Plugins`. If you see `_Flash Player.plugin` (with the underscore in front), delete that and restart Safari. That fixed the issue for me. I'm thinking that was some old version that, for some reason, was overriding the newer installed version (without the underscore). Strange, indeed.

Reference: [Relevant Apple Support Thread](https://discussions.apple.com/thread/4251341?start=0&tstart=0)
