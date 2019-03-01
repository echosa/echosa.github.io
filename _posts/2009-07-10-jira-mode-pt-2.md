---
title: "jira-mode pt. 2"
date: 2009-07-10
categories: [blog]
tags: [emacs, jira]
---
Well, folks, you asked and I'm delivering! I've creating a page on EmacsWiki for [jira-mode](http://www.emacswiki.org/emacs/JiraMode). There you will find information, instructions, and a link to the source code!
<!--more-->
Many thanks go to Dave Benjamin, who first wrote jira.el and has allowed me to improve it and, basically, take over the project code and wiki page.

A bit of a bad news, though. As stated in the known issues section of the wiki page, XMLRPC (which jira-mode uses) does not support all functions, for instance, resolving tickets or changing status. There is nothing I can do about this. Therefore, as long as jira-mode uses XMLRPC, these abilities will never be available.

However, many other functions are there, and are quite usable and just a keystroke away! I figure I spend more time working on tickets (i.e. creating, commenting, assigning, etc.) than closing them anyway, so jira-mode still has some use.

So, please, check it out and let me know what you think! If anyone wants to improve on it, let me know as I am definitely interested. Also, if anyone wants to convert jira-mode to use SOAP instead of XMLRPC, by all means do! Supposedly, Jira allows SOAP access to the functions that XMLRPC can not perform.
