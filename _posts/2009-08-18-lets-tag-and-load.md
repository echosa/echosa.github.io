---
title: "Let's Tag and Load!"
date: 2009-08-18
categories: [blog]
tags: [emacs]
---
Not too long ago, I learned the wonders of using tags for programming projects, in my case, PHP applications. I read [an article](http://weierophinney.net/matthew/archives/134-exuberant-ctags-with-PHP-in-Vim.html) (geared towards VIM, actually) that talked about tags and how they can be used for completion, reference, etc. I was intrigued and looked into using tags for Emacs.
<!--more-->
Before I knew it, I had tagged a project and was able to auto-complete function and variable names and could even jump to a function definition if I forgot its arguments or just needed to see its code! Very handy. However, I realized that every time I switched projects, I had to load the correct tags file. Sometimes I forgot and still have the tags for the other project loaded. Also, it was a pain having to manually load a tags file every time I switched projects. Sure, I could have one big tags file for all projects, but what if I have the same function name in both? Plus, that just seems like a waste of resources.

That prompted me to look for a way to auto-load the correct tags for a given buffer or file. I didn't really find any solutions, though I did find bits of code and script that helped me write my own. I figured I'd share this with you all so you can use or improve it.

First of all, I keep all my tags in one location, specifically a folder named "tags". I name them whatever the project is called. So inside "tags" I might have, for example, "app1", "myproject", "phpgame", etc. (All fake names, of course). I modified the linux script I got from the article above to make my tags:

```bash
#!/bin/bash
exec exuberant-ctags -e -f /path/to/tags/$1 \
-h ".php" -R \
--exclude="\.svn" \
--totals=yes \
--tag-relative=yes \
--PHP-kinds=+cf \
--regex-PHP='/abstract class ([^ ]*)/\1/c/' \
--regex-PHP='/interface ([^ ]*)/\1/c/' \
--regex-PHP='/(public |static |abstract |protected |private )+function ([^ (]*)/\2/f/'
```

This script will also work on Mac OS X. Windows users: sorry, you'll have to make your tags another way. You can modify this script to suit your own needs. Make sure you have exuberant-ctags installed (I don't use the etags that comes with Emacs) and check the documentation for how to change the script.

I named the script "tag-php". This script takes one argument: the tag file name to create. You go to to the top directory of the project in a terminal, and run:

```bash
$ tag-php tag-file-name
```

Next, I needed a way to get Emacs to load the tags for a buffer or file when I open it. That way, I'll always have the right tags for the file/buffer I'm current working on. In order for that to work, I wrote this bit of code in my .emacs file:

```cl
(setq tags-directory "/path/to/tags/")
(setq tag-list
  (list
   (cons '"/path/to/project1" (concat tags-directory "tags1"))
   (cons '"/path/to/project2" (concat tags-directory "tags2"))))

(defun load-tags ()
  (interactive)
  (if (buffer-file-name)
      (progn
        (dolist (tag-cons tag-list)
          (if (string-match (regexp-quote (car tag-cons)) (buffer-file-name))
              (progn
                (if (not (equal tags-file-name (cdr tag-cons)))
                  (progn
                    (message (concat "loading tags" (cdr tag-cons)))
                    (setq tags-file-name nil)
                    (setq tags-table-list nil)
                    (visit-tags-table (cdr tag-cons))))))))))

(defun switch-to-buffer-and-load-tags ()
  (interactive)
  (ido-switch-buffer)
  (load-tags))

(add-hook 'find-file-hook 'load-tags)
```

*Note that I typically only work on one file/buffer at a time, and only change to another via switching buffers or opening files. I never have two windows or frames with code open. That's why I only have the function running when I switch buffers or find a file. This function could probably be set to run when switching windows or frames, but I haven't tried it.*

Anyway, the last line hooks the "load-tags" function to "find-file" so tags are loaded whenever a files is opened. The function above that is a custom buffer switching function. Since I use [ido-mode](http://www.emacswiki.org/emacs/InteractivelyDoThings) and couldn't find an hook that would work (like the find-file-hook does), I wrote the function "switch-to-buffer-and-load-tags" and rebound the normal "C-x b" to perform that function instead:

```cl
(global-set-key "\C-xb" 'switch-to-buffer-and-load-tags)
```

Obviously, the "tags-directory" variable needs to be set to the path where the tag files are located. The "tag-list" variable is a list that associates project directories with their tag file. Just fill them in appropriately.

What happens here is that when I switch buffers or open files, load-tags looks to see if the directory of the buffer/file is one of the directories in "tag-list". If so, it loads the appropriate tags file, overwriting the previously loaded one so you don't waste resources.

Ok. You've got your tags file. You've got your directories and projects all set up in your .emacs file. You've loaded a file and the tags were automatically loaded. Now what?

The two main uses I get from tags are completion and reference. For this, Emacs actually has two built-in commands: "complete-tag" and "find-tag". I bind these to keys:

```cl
(global-set-key "\C-cj" 'find-tag)
(global-set-key [(control tab)] 'complete-tag)
```

When typing a function or variable name, "complete-tag" will attempt to complete the name. Simple enough.

However, "find-tag" is an interesting function. Let's say I define a function in a file. Then, in another file, I am using that function. If I put the point somewhere on the function name and call "find-tag" (which takes one argument: a tag name, in this case a function, and will default to whatever is under the point), Emacs will actually load the file where the function is defined, and put focus at the definition.

Its difficult to describe it in writing, so just go try it out! Its really neat and very handy. It's not perfect, mind you. I do suggest reading [what the GNU Emacs Manual has to say about using tags in Emacs](http://www.gnu.org/software/emacs/manual/html_node/emacs/Tags.html#Tags). There are more functions that I haven't covered (because I rarely make use of them).
