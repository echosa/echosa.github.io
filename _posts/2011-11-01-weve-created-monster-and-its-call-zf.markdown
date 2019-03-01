---
title: "We've created a monster... and it's call zf-mode!"
date: 2011-11-01
tags:
- emacs
- php
- zf-mode
---
Ok, so it's been quite a while since I've posted anything here. I've been busy. Sue me. However, I've been busy writing php apps with zf-mode. Why, you may ask? Because 1.) it's awesome, 2.) I'm testing it for bugs, and 3.) its the single most useful emacs mode I've ever used.
<!--more-->
Here's the exciting part: I think we're getting really close to a release! I still don't have a date, but it's definitely coming. Prepare yourselves; this is not the little zf-mode you knew before. Here's just a few of the new abilities you can look forward to:

*  Automatic, correct line/statement breaking (with customizable options)
*  Integrated support for php testing using phpunit, phpcs, and phpmd
*  Easy navigation between files and parts of files (methods, properties, etc).
*  Project handling
*  So much more....

We're really excited about releasing zf-mode, but we really want to make sure we have as many bugs worked out as we can find prior to release. We're working on the last couple of features we want for the first release right now, so it can't be *too* long before the release. Please, be patient.

Also, just as a side note, zf-mode is now its own major-mode, no longer dependent upon using php-mode. zf-mode is currently well over 7000 lines of code (actual lines of code, not including comments or blank lines). Its hard to believe its come so far since its initial creation back in 2008 as a single function to insert a Zend_Debug::dump() statement with or without a die afterwards. My little program is all grown up!
