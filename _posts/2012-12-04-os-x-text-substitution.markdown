---
title: "OS X Text Substitution"
date: 2012-12-04
categories: [blog]
tags: 
- mac
---
The last couple of versions of OS X have had a cool feature: user-added text substitutions. Meaning, you can set some placeholder text (like "lod") that will be auto-corrected to something else (in my case, the [Look of Disapproval](http://www.disapprovallook.com)).
<!--more-->
You can add your own text substitutions by going to `System Preferences -> Language & Text` and clicking on the Text tab. Click the + at the bottom left to add a new one, then choose what you want to type and what you want it to be replaced with. Make sure that "Use symbol and text substitution" and "Correct spelling automatically" are checked. (The latter is only necessary if you want OS X to do so; if you'd rather do it yourself, you can leave this off I guess.)

At this point, if you're like me, you'll think you're good to go. You'll go to Mail or Textedit and try it out, and it will work. You'll then go to, for instance, Messages and try to use your new substitution only to find out that it *doesn't* work! This frustrated me to no end, until a friend pointed out the missing piece of the puzzle. 

Apparently, each application can determine its use of text substitutions. If your substitutions do not work in a particular application, simply go to `Edit -> Substitutions` and make sure that "Text Replacement" is checked. Now your substitutions should work! (Go ahead, try it!)
