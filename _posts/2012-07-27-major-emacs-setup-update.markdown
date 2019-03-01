---
title: "Major emacs-setup update!"
date: 2012-07-27
tags:
- emacs
---
I recently updated my [emacs-setup package](https://github.com/echosa/emacs-setup) (available through [MELPA](http://melpa.milkbox.net/)) and made some major changes!
<!--more-->
First, emacs-setup no longer handles window/frame management or layout. There are other packages out there that do this much better than I, including revive.el and my new favorite toy e2wm.

Secondly, emacs-setup-elisp-base-dir is now emacs-setup-require-base-dir, and emacs-setup-elisp-ignore-dirs is gone. I also got rid of the pre-sexp and pre-layout-sexp variables.

The most exciting part is how easy it is to use now! Instead of the several lines of code needed before, now all you have to load is include a (load-file /path/to/emacs-setup.el) in your .emacs.

The other remaining features have been improved as well:

* adding/removing packages from being required during setup
* adding/removing extra load-path directories
* adding/removing PATH entries
* adding/removing keybindings (when binding a function to a key, the functions list now completes)

Much of the improvement is internal, but I have fixed several bugs and made some of the interactivity better. Either way, this is a major release, and I'm quite excited for it.
