---
title: "Press 'q' to quit, 'z' to *really* quit."
date: 2012-08-30
categories: [blog]
tags:
- emacs
---
Does it ever bug you that when you press 'q' to quit a buffer, like *Help*, it doesn't actually quit but, rather, buries the buffer? Well it bugged me and I looked into the matter. Turns out the answer is right there in front of you, but not very obvious... z!
<!--more-->
Looking closely at the keybindings of, for instance, the *Help* buffer (with C-h m), I noticed that 'z' was bound to a kill function. Interesting. Turns out that pressing z will actually kill the buffer. So if you're actually done with it and want it gone and not cluttering your buffer list, use 'z'  instead of 'q'.
