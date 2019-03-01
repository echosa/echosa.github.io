---
title: "zf-mode is no more... Viva php+!"
date: 2012-05-25
categories: [blog]
tags: [emacs, php, zf-mode]
---
My emacs package for working with php has just undergone a significant change. It is no longer called zf-mode.
<!--more-->
Introducing: php+-mode!

PHP+-mode is just that. Its a mode for working with PHP files, *plus* other things (including some Zend Framework support [which is where it got its original name from]).

You can find it at [https://github.com/echosa/phpplus-mode](https://github.com/echosa/phpplus-mode). If you already use zf-mode, I suggest deleting it and getting php+. However, bear in mind that there have been changes to the names of customized variables. Please update (or reset) these accordingly.

If you use zf-mode and got it from MELPA, bear with me. I have submitted a pull request to the MELPA github with a new recipe for php+. Once that has been accepted, you'll be able to download php+ from MELPA once again.

In other news, I have just discovered the awesomeness of snippets via yasnippet.el. This has opened a *whole new world* to me, and means some big changes to php+. I've already begun working on some major usage improvement using snippets that will make php+ a lot easier to use and, in my opinion, a lot more fun.

Stay tuned for more details on php+!

Finally, I learned about yasnippet from [@EmacsRocks](http://twitter.com/#!/emacsrocks) on Twitter. EmacsRocks puts out [videos](http://emacsrocks.com/) show casing some of the cool things you can do with emacs. I highly recommend you check them out; they're typically only a couple minutes long.
