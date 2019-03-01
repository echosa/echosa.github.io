---
title: "PHP and chmod"
date: 2012-09-27
categories: [blog]
tags: [php]
---
So, here's a tip that would have saved me about 10 minutes of frustrated work today. As [clearly stated in the PHP manual](http://php.net/manual/en/function.chmod.php), when you're setting the mode for a file via a number, the number must be expressed as octal. What this means is that the leading zero that is typically implicit when using chmod from the command like (e.g. `chmod 777 <file>`) is **not** implicit when calling chmod from PHP. You have to supply the leading zero, meaning you call something like `chmod(<file>, 0777)`.
<!--more-->
Now, you might be wondering why someone would be calling chmod from PHP anyway. I know I would be. Well, I'm doing so for testing purposes. I have begun using [Behat with the Mink extension](http://behat.org) for behavioral testing. I have an sqlite database that gets used with test data for these tests (the actual application uses MySQL, and yes, keeping those two in sync is a pain, especially when triggers are involved, but I digress). 

Anyway, because of the way Behat works in conjunction with my running Apache/PHP/application setup, I didn't see a way of hooking into Behat in such a way where I could tell the database to run everything in throw away transactions in order to keep my database clean and as expected for each test scenario. Therefore, I simply hooked into Behat before each scenario to copy my pristine test database to a backup, then after each scenario copy it back, essentially rolling back any transactions that occurred during that scenario.

This may not be the best way to do it, but its what I figured out and its working for me, for now at least. Luckily, this is a well established application and the database doesn't change, so the mysql <-> sqlite syncing is a null issue for the foreseeable future.
