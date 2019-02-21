---
layout: post
title: "Seek and Hide"
date: 2009-12-21T14:49:00-08:00
comments: true
tags:
- emacs
---
Recently I've found myself using [HideShow](http://www.emacswiki.org/emacs/HideShow) more. Its a package that makes it easy to hide or show blocks of code. However, I found it a bit lacking in a particular manner. I wanted to be able to hide all PHP doc blocks and the contents of all methods in a class. There's no one command in HideShow to do this, so I wrote my own (and then added it to my php-mode hook).
<!--more-->
 Here's the code:

```cl
(defun hide-class-contents ()
  (interactive)
  (save-excursion
    (beginning-of-buffer)
    (while (re-search-forward "[ \t]+{\\|/\\*\\*" nil t)
      (hs-hide-block)
      (move-end-of-line nil))))
```

To really get a feel for what this function does, get HideShow and use it a bit, then use my function. You'll see that HideShow can do a "hide all", but in a class that simply hides everything in the class. You can do a "hide level" inside a class, but that will hide all the function's contents, but not the doc blocks. It also *will* hide the arguments to a function if they are on multiple lines. My function is, in my opinion and for my usage at least, cleaner and more exact in what i want to hide (or not hide) when first opening a php code file.

You might notice that in the regexp, I search for opening curly braces with at least one space or tab in front. I do this to bypass the opening class brace, since hiding that will hide everything in the class. Of course, this regexp can be change to meet your coding style. I put my class and function opening curly braces on the line below the definition, like this:

```php
<?php
class SomeClass
{
    function someFunction()
    {
    }
}
```

If you code like this instead (which I used to):

```php
<?php
class SomeClass {
    function someFunction() {
    }
}
```

you can change the regexp to search for something like

```
"\\(function\\)[ \t.]+{|/\\*\\*"
```

I haven't tested this, but it gives you an idea for a starting point, at least. Don't take it as a copy/paste, as its probably wrong.

Of course, there's nothing saying this only for PHP, as HideShow is generic. I find this function useful and hope others will too.
