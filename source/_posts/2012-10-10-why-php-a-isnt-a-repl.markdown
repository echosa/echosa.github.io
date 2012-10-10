---
layout: post
title: "Why the PHP Interactive Shell Isn't a REPL, and Why It Is Lacking"
date: 2012-10-10 09:23
comments: true
categories: 
- php
- repl
---
After a recent conversation on Twitter, I felt like I should explain why I feel that `php -a`, the PHP Interactive Shell, isn't a REPL, and where it falls short because of this.
<!--more-->
First, a disclaimer: I will be giving a local talk on REPLs later this month, so if you will be attending that, there's no need to read further. I'll be going over pretty much everything in this post during my talk, so please, come by and attend! *end shameless self-promotion*

...

Still here? OK, then. Moving on.

Let us start with a definition of sorts. REPL stands for Read-Eval-Print-Loop. A REPL is a program that reads input, evaluates what it read, prints the result (and possibly any output, and yes, there is a difference), then loops back to the read stage awaiting more input to evaluate and print. Here's an example session in the REPL for ruby (irb):

```
$ irb
1.9.2p320 :001 > 1
 => 1 
1.9.2p320 :002 > 2
 => 2 
1.9.2p320 :003 > 1+2
 => 3 
1.9.2p320 :004 > ohai
NameError: undefined local variable or method `ohai' for main:Object
           from (irb):4
           from /Users/bzwahr/.rvm/rubies/ruby-1.9.2-p320/bin/irb:16:in `<main>'
1.9.2p320 :005 > "ohai"
 => "ohai" 
1.9.2p320 :006 > print "ohai"
ohai => nil 
1.9.2p320 :007 > def printOhaiAndReturn42
1.9.2p320 :008?>   print "ohai"
1.9.2p320 :009?>   return 42
1.9.2p320 :010?>   end
 => nil 
1.9.2p320 :011 > printOhaiAndReturn42
ohai => 42 
1.9.2p320 :012 > quit
```

As you can see, the REPL takes the input, then prints the evaluation. Notice that the result of the evaluation is printed after a double arrow (=>). irb makes a distinction between result and output using the double arrow. In the example I define a function that prints a string (ohai) and returns a number (42). Running the function results in `ohai => 42`, showing us that `42` is the *result* of the evaluation while `ohai` is what would be output (in this case to stdin). We also see an error when I try to evaluate the string `ohai` without quotes. The REPL tries to evaluate it as a variable or function, which of course it isn't, and gives us an error stating this.

This is a typical REPL. Some REPLs are different. For instance, python doesn't show different result and output values. Different REPLs handle multiline input (like when I defined the printOhaiAndReturn42 function, above) in different ways.

The PHP Interactive Shell is not typical REPL. I dare say its not a REPL at all. Here's a similar session to the irb example above, this time in the PHP Interactive Shell:

```
$ php -a
Interactive shell

php > 1
php > 2
php > 1+2
php > ohai
php > "ohai"
php > print "ohai"
php > 1;
PHP Parse error:  syntax error, unexpected '2' (T_LNUMBER) in php shell code on line 2

Parse error: syntax error, unexpected '2' (T_LNUMBER) in php shell code on line 2

php > 2;
php > print "ohai";
ohaiphp > function printOhaiAndReturn42 () {
php { print "ohai";
php { return 42;
php { }
php > printOhaiAndReturn42();
ohaiphp > 
php > 1
php > +2
php > +3;
php > print 1
php > +2
php > +3;
6php > quit
```

Right off the bat, you should notice two things: there's a lot less printing going on, and when something is printed there's no implicit newline (meaning the printed output is immediately followed by the next prompt). A larger but less immediately noticeable difference is that the shell requires a semicolon at the end of its statements (not a shock since this is PHP), so the first seven lines of the example are all evaluated as one statement (which is obviously invalid, thus the following error). This is also demonstrated on the last four lines, where I evaluate `print 1+2+3;` on several lines, thus getting 6 as output. The three lines prior to those, I make the same arithmetic evaluation but without calling `print`, which means I don't actually see my output.

This leads to a big issue with the shell. It doesn't let you know via the prompt that you're continuing the same statement as the previous line(s). Notice that when I defined the function, the prompt changed to have an opening curly brace while I was inside the function defining it. That's nice, and you can see that irb did something similar by adding a question mark to the prompt. Of course, you would think that as long as the shell doesn't show you any output or results that you could implicitly know that you are continuing a multiline statement. However, since the shell doesn't output anything even after a statement is ended with a semicolon, unless you explicitly told it to `echo` or `print`, that's just not true.

So, I've come to the conclusion that the PHP Interactive Shell isn't a REPL, its a REL. There's no implicit or expected Print stage of the loop, as there is in a typical REPL.

Also, in order to be called a REPL, you should be able to input any valid statement, variable, scalar, etc. and have it evaluated (with or without a semicolon). If I put `1` in, I should get `1` returned and see that return value printed by the REPL. Sure, there's no semicolon, but when PHP is evaluating something like `print 1+2;`, it still has to evaluate what `1` and `2` are individually in order to treat them properly. This, of course, would require the Interactive Shell to make one of two changes: either force all regular statements (not class or function definitions, for instance) to be on a single line (thus removing the need for an ending semicolon as it it would be implied), or add some way of specifying that you want to continue this statement on the next line (like using \ in multiline bash calls). If the latter is the solution, then the prompt should definitely reflect this. I think I would prefer the former, since that is how most typical REPLs work. What you put as input, unless it is something that absolutely requires more input (like a function call without a closing parenthesis or a class or function definition that hasn't been closed with a closing curly brace yet) is immediately evaluated when you press return. Want to evaluate 1+2+3 like in the example? Then input `1+2+3` all on one line.

There's more to REPLs and the Interactive Shell than this, of course. This was just a quick overview of why I feel the PHP Interactive Shell is lacking. That's not to say it is a useless tool. It has its place and uses, but I would like to see it be an actual REPL instead.