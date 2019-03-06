---
title: "Learning and Using the Standard Editor"
date: 2019-03-06
categories: [blog]
tags: [ed]
---
It's no secret that I enjoy text editors. Emacs. Vim. Acme. Even modern editors like VS Code. I don't know why, but I just really like learning and using them. I've even written about them many times on this blog. So it shouldn't surprise anyone that I would turn my attention to ed(1) at some point.

Well, that point is now. For a few months, I've been learning to use, and actually using, ed(1) (which I'll just refer to as ed for the rest of this article). Ed pre-dates most other text editors. It was used before monitors were even a thing, when computer output was all printed on paper. It was the main editor used while things like Unix were being created. Because of this history and heritage, ed has been given the moniker of the Standard Editor.

Of course, calling it that at this point is half true, half tongue-in-cheek. While there is some claim for it, the entire idea of it has become something of a [joke](https://www.gnu.org/fun/jokes/ed-msg.txt). You can see countless posts across the Internet, especially on Reddit, claiming ed's standard-ness, both as a joke and as a serious topic for discussion. I don't make any claims of it being "standard", but I do claim that it is still relevant and useful today.

It's easy to overlook ed or pass it up. It's old. It's weird. It seems really useless at first glance. Honestly, for many things, I'd say it is useless. I wouldn't use it to program a giant Symfony project in PHP, for sure. My IDE is too helpful to give up for even newer editors like VS Code, let alone something like ed. However, for quick edits (like editing dotfiles) or plain-text writing (like this post), ed is actually quite good at what it does! This post is being written in ed right now, in fact. Even more than that, almost everything I've done since reviving this blog has been done using ed.

Describing ed is a bit tricky. The best way to really understand it is to use it. So, to everyone reading this, I recommend giving ed a shot. Even if you hate it or never use it again, I think it's a good exercise to learn it. You'll gain a new way of thinking about editing text, you'll gain new skills and a new appreciation for regular expressions, and, if nothing else, you'll learn first-hand about some important computer history.

So, where to start? Well, install it.  Most (but not all) Linux distributions already have ed. macOS also has ed, but it is the BSD version. I prefer GNU ed, which I installed on macOS through [Homebrew](https://brew.sh) with `brew install ed`. I'm not sure about Windows. I imagine there's a version of ed for Windows, or maybe it needs to be run with Cygwin or Windows 10's built-in Linux subsystem.

Next, I recommend reading the man page. If it didn't get installed, you can always [find it online](https://www.systutorials.com/docs/linux/man/1-ed/). This will give you a brief explanation of how ed works but honestly doesn't serve as a good teaching tool for new users. For that, I recommend the following three resources. 

First and foremost, I recommend the book [Ed Mastery](https://www.tiltedwindmillpress.com/product/ed/) by Michael W. Lucas. Not only is it a wonderful and modern teaching tool for ed, the author's writing style makes it fun to read! I had difficulty putting this book down like it was a fiction novel. Seriously. This book is worth every penny, I promise. 

If you're looking for something a little less lengthy, there's a wonderful blog post from 2012 by Tom Ryder called [Actually using ed](https://sanctum.geek.nz/arabesque/actually-using-ed/). I read this before I bought Ed Mastery, and it was a great "quick start" of sorts. 

Finally, the Twitter account [@ed1conf](https://twitter.com/ed1conf) has been very helpful in answering any questions that I've asked. Keep in mind, that's not some sort of official support Twitter account or anything. It's just some person (as far as I know) who has has taken the time to help me, for which I am extremely grateful. I only mention this because I don't recommend flooding the account with questions.

I could continue here by trying to explain ed, showing how it works, etc. I won't do that, though. I feel I couldn't do it justice, and the resources I've already mentioned are way better than anything I would produce here. I will repeat this, though: ed is best learned by doing. Install it. Run it. Try it! 

If you do try ed, or if you already use it, I'd like to hear about it! Leave a comment here or on [Twitter](https://twitter.com/echosa). I've already have several conversations about ed on Twitter, actually, and I've seen other people comment the same thought I've had: I didn't realize how big of a following/user base ed still has! My tweets about ed have been some of my most reacted to and responded to. That still amazes (and amuses) me.

ed, man! !man ed
