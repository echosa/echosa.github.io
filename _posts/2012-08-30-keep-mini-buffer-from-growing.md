---
title: "Keep the mini buffer from growing"
date: 2012-08-30
categories: [blog]
tags: [emacs]
---
Often, when doing things like switching buffers, the minibuffer will grow beyond its normal height of 1. This has been bugging me lately, so I sought out a way to fix it.
<!--more-->
This may not be the best way, but setting this:

```cl
(setq resize-mini-windows nil)
```

seems to do the trick. Note that its simply truncates whatever text is in the minibuffer, but I'm OK with that. For now.
