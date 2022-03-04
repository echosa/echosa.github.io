---
title: "Quick Save with Git"
date: 2022-03-04
categories: [blog]
tags: [git, programming]
---
A feature that video games players are very aware of and often use is something called "quick save". Quick save allows you to save your game, anytime and anywhere, so that you can always come back to that spot via a "quick load". For instance, if you're about to fight a boss, you can quick save right before the fight. That way, if you lose, you can just quick load back to that same spot without having to trek all the way back to the boss after losing and being put back at the beginning of a level. This is very useful and a huge time-saver.

As software developers, we can get similar usefulness in our development using `git`! Bonus: it's actually very easy to do! So how does one achieve this? Simple: **commit changes often**.

That's it!

No, really. That's all there is to it!

How does commiting often give "quick save" benefits? Let me give an example!

Let's say I'm writing some code and I start by writing a test. TDD is still a thing people do, right? I write a failing test (failing because I'm writing the test first). I now have two options. I can either:
- continue immediately on to writing code to make the test pass, or
- commit my changes before doing so

I decide I want to "quick save", so I commit my changes to git. (Note: I'm talking about commiting locally. I'm not pushing anything to a remote, like Github, yet.) Once I've done that, I start working on making the test pass.

I write some code, run the test, and see it's not working. I realize I completely went about my solution in the wrong way, so I need to redo the work.

It's time to "quick load"! Instead of having to manually find and undo all my changes, I can simply `git reset --hard HEAD`, and I'm right back to exactly where I was: a written by failing test, waiting for me to make it pass. So I try another solution. This one also doesn't work, so I quick load and try again. 

Hopefully you can see the convenience `git` is providing me, but the benefits do not stop there! There's another reason I commited the test first before moving on

Let's say I hadn't commited the test. Instead I wrote the test and immediately started working on the code to make it pass. The code doesn't work, so I want go undo it. However, I do not want to undo the test. So, I have to manually go undo all my non-test changes to get back to where I was after writing the test but before working on the code to make it pass. If I'd just commited the test first, then this wouldn't be an issue! I'd just quick load with `git reset`. Done!

Let's keep going, though. I've written the test and committed it. I've make the test pass. I can now commit that code for a new "quick load" point. By commiting the changes, I essentially give myself a clean slate for the next changes and an easy rollback if needed. So, I write another test, commit it, make the test pass, commit it, etc. 

To complete the video game analogy, often video games give you multiple "save slots", essenatially you ccan have multiple saves stored at once which you can load at will. Perhaps I save at the beginning of a level, then halfway through level after finding an item or secret, and then right before the boss. If I need to, I can go back in time to any of these positions, giving myself a redo, essentially.

Commiting changes in small, complete batches gives this same effect. Every git commit is basically a save point that you can always load.

I will say, it can be weird to put this into practice at first, for a couple of reasons. The first is that you have to change the way you think. Instead of thinking of an entire coding project or task as one atomic unit, you have to think about how you can break it down into smaller, atomic units that can be completed and commited individually. Second, you have to get into the habit of remembering to commit between each of these smaller atomic units of work.

I believe everyone can benefit from adopting this quick save/quick load model into their workflows. It adds very little in terms of overhead and additional time while providing significant benefits.

Hopefully, someone who reads this gets use out of my suggestions! Happy coding!
