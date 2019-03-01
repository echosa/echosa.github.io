---
title: "Emacs with TRAMP Causing OS X Kernel Panic"
date: 2013-02-01
tags: 
- emacs
- mac
---
I've had a couple of kernel panics while using my MacBook lately, and I have figured out the culprit. It's Emacs, specifically when using TRAMP (in my case, to open a file via sudo).
<!--more-->
So, here's the deal. I'm running OS X version 10.8.2 on a 15" MacBook Pro with Retina Display and have Emacs version 24.2.1 installed with [Homebrew](http://mxcl.github.com/homebrew/) without GUI support since I run Emacs via terminal. On this setup, I can reproduce my issue without fail. Here's how to do so (careful if you try this as it could cause a kernel panic):

1. Open Emacs (might have to be in a terminal, which can be forced with `emacs -nw`)
2. Open a file with TRAMP, in my case for sudo access. To do this, if you are using ido-mode, then type `C-x C-f` and type `//sudo:root@localhost:/` (note the double forward slash at the beginning) and you should be asked for your password. After you give you password, finish typing the file name (in my case, `etc/php.ini`). If you aren't using ido-mode, you only need to type `C-x C-f` followed by `/sudo:root@localhost:/etc/php.ini`).
3. Now that you have a TRAMP process running, exit Emacs. 

If you have the same issue as me, exiting Emacs will cause a kernel panic. Killing the buffer prior to exit doesn't help, and neither does killing the TRAMP buffer that opens. However, actually killing the TRAMP process allows Emacs to close properly. This can be done by finding the process in via `M-x list-processes` and using `(delete-process PROCESS-NAME)` to kill it.

Of course, when OS X kernel panics, you get the option to send an error report to Apple. I saved the panic report to a text file and examined it. The error given by the kernel is as follows:

```
panic(cpu 2 caller 0xffffff802491ec9a): "negative open count (c, 16, 1)"@/SourceCache/xnu/xnu-2050.20.9/bsd/miscfs/specfs/spec_vnops.c:1813
```

Later is the very long panic report, I see

```
BSD process name corresponding to current thread: sudo
```

which is what caused me to investigate TRAMP as the issue.

Honestly, I don't know what's happening, and intend to do some Google searching to find out. If anyone has any information, please share. Otherwise, I advise everyone to be careful using TRAMP in the near future.
