---
title: "CLI Emacs and multiple-frames"
date: 2012-10-08
categories: [blog]
tags: [emacs]
---
So, I've been using the CLI Emacs again, because I'm fickle like that. Anyway, I've gotten used to have two frames: one with my code in a few windows and one with a few windows holding magit, compilation buffer, a term, etc.

Turns out that you can have multiple frames even in CLI Emacs. C-x 5 2 creates a new frame, C-x 5 o switches between frames. You'll notice that the mode-line of the first frame has an "F1" and the second has "F2". Also, you can run M-: (frame-list) to see the frames you currently have.
