---
title: "Kill Multiple Lines with kill-lines"
date: 2012-10-16
categories: [blog]
tags: [emacs]
---
Today, I wrote an Emacs package called `kill-lines`. It is a simple package with an interactive function of the same name that, when run, allows the user to enter a line number and kills all lines from the current line to the given line (inclusive). To make this easier, it turns on highlighting of the current line (so you can see where you're starting from) and line numbers (so you can easily pick one as the target). It turns these visual aids off when it is done, unless you already had them turned on to begin with.

Of course, you can bind kill-lines to a keybinding. I have chosen C-c C-k.

You can find kill-lines at my GitHub repo [here](https://github.com/echosa/emacs-kill-lines).
