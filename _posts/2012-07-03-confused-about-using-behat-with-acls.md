---
title: "Confused about using BEHAT with ACLs (and ACLs in general)"
date: 2012-07-03
categories: [blog]
tags: [php, behat]
---
A bit of disclosure before I begin. I'm completely new to behat, so I have little knowledge of it beyond what little bit of work I've done with ecukes (which is basically Cucumber for Emacs). That said, I'm trying to setup behat to test various parts of a web application I am writing. Specifically, I have a really, really long form that I'm tired of manually filling out and submitting in the browser. However, I believe I'm running into an issue accessing the form's page in the first place.
<!-- more -->
The application is using Zend Framework 1.11, and with that I'm using Zend_Acl and Zend_Navigation to auto-generate menus and breadcrumbs, as well as restrict access to parts of the application via ACL roles. Its the latter that I believe is causing me issues. What happens in the application is whenever a page is requested, the application looks at the currently logged in user (stored in the session) and retrieves the user's role. The role is then checked against the Zend_Navigation config, which assigns a resource to every page. This user role and page resource are checked with the ACL to find out whether or not the role is allowed rights to the resources. Basically, all basic ACL stuff.

So, to my concern. I need a way to let behat run the page with the form, which of course requires a particular ACL level. My first question is should I be checking my ACL at a different time/level of the application? By this, I mean to say should I make it so that the controller action itself can be reached no matter what (thus, freely available to behat), but somehow deny actual users access, menu items, etc. another way? 

My second question is, if the application remains the way it is, what is the best way to "log a user in" via behat. I'm assuming I should make a step definition that creates a user object with a certain role and adds that to the session. Fair enough. However, due to some bad coupling that I can't handle just now (but will handle soon-ish), I need more than just my user model. Which brings me to...

How do I set up my autoloading in Behat? When I simply require_once for my user model, the other classes can't be found (obviously). 

So, I will continue investigating this issue, but please, if you have any useful information for me, comment or contact me in some other way (if you have the means). I'd really like to get this underway to improve my life just a little bit.
