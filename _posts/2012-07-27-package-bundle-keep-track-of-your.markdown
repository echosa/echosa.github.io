---
layout: single
title: "package-bundle: Keep track of your dependencies!"
date: 2012-07-27T14:20:00-07:00
comments: true
tags:
- emacs
---
I have just pushed a new project to my github account: [package-bundle](https://github.com/echosa/package-bundle). It acts *sort of* like Vundle for vim, etc. It keeps track of your installed packages/dependencies (installed via package.el of course) and allows you to install them all with one command.
<!--more-->
Why, you ask?

Well, I get tired of having to commit/push every time I install or delete a package via package.el. I already have my emacs config in github for version control and cloned into my Dropbox. This way, whenever I install or change something, it propagates to my other machines. However, if I have to install my config on a new machine, that doesn't have access to my Dropbox (for any reason), I can just clone it. However, in order for this to work, I had to keep all of my package.el packages stored in github as well, which caused a flurry of commits/pushes each time I installed or deleted a package.

package-bundle to the rescue! Instead of keeping all the installed packages themselves in github, I just keep package-bundle.el and my package-bundle file (which holds the references to the packages I need/want installed). I clone my config, load package-bundle, make sure that package-bundle-file points to the correct file (via customize), then run package-bundle-install. Assuming that package.el and the repositories (including the network connections between me and them) work just fine, all my wanted packages will be installed and ready to go (admittedly, after a bit, since package.el can be a bit, er, slow).

Bear in mind that this project is still *very* young. I encourage you to try it out and give me feed back (forking the project and submitting issues and/or pull requests on github would be *great*), but do make sure you back everything up first. Just sayin'.
