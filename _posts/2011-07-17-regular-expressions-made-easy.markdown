---
title: "Regular Expressions made easy!"
date: 2011-07-17
tags:
- emacs
---
I'm still fairly new to regular expressions. I've read many tutorials and web pages on how to use them, and while I understand and remember a lot of what I read, I often find myself using regular expressions incorrectly. I often find myself writing a regular expression, testing it, finding out its wrong, and starting over.
<!--more-->
Once again, emacs has come to my rescue! There is an emacs function called `re-builder` and it is a life saver when it comes to building regular expressions. Say you're in a buffer and trying to write a regular expression to match certain point(s) inside the buffer. Just run `M-x re-builder` and you'll get a small window below the one you're in. That is the re-builder window. It should be empty except for two double-quotes.

You can begin typing a regular expression in between the quotes and the appropriate matches to the expression will be instantly highlighted and filtered as you type! If you have any sub-expressions, they'll even be highlighted in different colors so you can see exactly what each sub-expression is matching! If you type something that is wrong, you'll know immediately since the correct match will no longer be highlighted in the buffer. Once you have the perfect regular expression, you can simply copy and paste (*ahem* sorry, kill and yank) it to where you need it, be it a function you're writing, input to an interactive function call via M-x, or somewhere else.

There are a couple of things to remember when using re-builder. If you start a grouping (brackets) or a sub-expression (parentheses), nothing will be matched or highlighted in the target buffer until you close it. So, when you're writing those, don't think its all wrong when all the highlighting goes away. re-builder just can't match anything until you close off the expression.

Secondly, when working in re-builder, you'll need to escape backslash. For instance, sub-expressions would be \\(...\\) as opposed to \(...\). However, if you are going to use the finished regular expression as an argument to, say, M-x query-replace-regexp, you'll need to remove the extra slashes (and the beginning and ending quotes, for that matter).

Also, if you need to match a newline, you can do so with [\n]. The \n needs to be in a grouping brackets. However, once again, if you'll be using the expression with, for instance, M-x query-replace-regexp, after you put the expression into the minibuffer, you'll need to delete the \n and type C-q C-j to put a literal newline in its place.
