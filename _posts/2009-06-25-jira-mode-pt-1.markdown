---
title: "jira-mode pt. 1"
date: 2009-06-25
categories: [blog]
tags:
- emacs
- jira
---
Well, folks, it's been only a matter of time. I've begun working on my first major mode project. Where I work we use [Jira](http://www.atlassian.com/software/jira/) for bug tracking, ticketing, and support requests. Naturally, like any obsessed emacs user, I found myself wondering "how can I work with Jira without leaving emacs?" Of course, the first obvious answer was to use the Jira web interface via the w3m web browser in emacs. However, not everything worked.
<!--more-->
So, I did what I always do in situations like these: I went to [EmacsWiki](http://www.emacswiki.org). After a quick search I found [jira.el](http://www.emacswiki.org/emacs/jira.el), an elisp file for working with Jira via XMLRPC written by Dave Benjamin. I tried it out, and it worked. It is quite incomplete, though. Therefore, I decided to start adding to it.

For instance, it could get the information for a ticket, but couldn't add comments or even add new tickets. I started adding all this functionality and found myself thinking it would be great to have a jira-mode that I could set in a buffer where I could do things like press "r" to refresh a ticket, "c" to create a new one, etc. I looked around, and noone else seems to have made anything like this, so I decided I would.

As of now, I have a working mode, with some customizable faces, that can create tickets, refresh tickets, update tickets, list projects, and a few other basic functions. I am adding more and more to jira-mode and will definitely keep an update on it. I will probably re-post it back to EmacsWiki at some point. For now, I just want to get it useable and practical.

That said, I have to say, its incredibly easier to write a major mode than I had anticipated. Of course, the more complicated the application, the more complicated the mode will be to write. I'm rather pleased with what I've done so far and, as I've said, will post updates about jira-mode here as I make more breakthroughs.

So, keep an eye out for pt. 2!
