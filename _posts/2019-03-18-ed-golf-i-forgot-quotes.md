---
title: "ed Golf: I Forgot Quotes"
date: 2019-03-18
categories: [blog]
tags: [ed]
---
Well, since the [previous ed golf]({{ site.baseurl }}{% post_url 2019-03-11-ed-golf-one-number-per-line %}) was so much fun and such a hit, especially on Twitter, let's keep doing more! Today, the challenge is a pretty simple one. How low of a score we can get on [I Forgot Quotes](http://www.vimgolf.com/challenges/5462e3f41198b80002512673)?

```
$ ed
### Insert start file
i
foo = a
      ab
      abc
.
####################
### GOLF STARTS HERE
####################
### 16 - Insert quotes
,s/\(a.*\)/"\1"
      "abc"
####################
### GOLF ENDS HERE - Total: 16
####################
### Output result
,p
foo = "a"
      "ab"
      "abc"
```
I was able to do this one with just a single substitution command for a score of 16. I think that's pretty good! I just search for `a.*` and wrap all results in quotes - easy peasy!

However, looking back at it, I wonder if it would be less keystrokes to run two simpler substitutions rather than a combined one. Let's find out.

```
$ ed
### Insert start file
i
foo = a
      ab
      abc
.
####################
### GOLF STARTS HERE
####################
### 8 - Insert starting quotes
,s/a/"a
      "abc
### 7 - Insert ending quotes
,s/$/"
      "abc"
####################
### GOLF ENDS HERE - Total: 15
####################
### Output result
,p
foo = "a"
      "ab"
      "abc"
```
Well, look at that! 15 strokes - one less than the combined substitution! Perhaps clever is not always best.

Is there a way to get a score of less than 15? I'd love to know! Comment below or [on Twitter](https://twitter.com/echosa).

Also, if you're enjoying these ed golf posts, let me know! I'm certainly enjoying them, but I'll definitely keep them coming if you do, too!
