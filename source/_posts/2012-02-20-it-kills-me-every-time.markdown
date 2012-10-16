---
layout: post
title: "It Kills Me Every Time..."
date: 2012-02-20T22:37:00-08:00
comments: true
categories:
- emacs
---
I *always* forget about the kill ring, or rather I used to. I've made a habit of using it lately. Its just so damn handy, I don't know why I could never grasp it before.
<!--more-->
For those who don't know, anytime you copy or "kill" text in an emacs buffer, its get placed on the kill ring. This includes certain basic functions like kill-word. So, often, I would copy some text I wanted to use to replace some other text (we'll say a word, for example), then kill the word I want to replace. This would mean that when I yanked the text (ctrl-y, basically emacs' paste), it would insert the last thing killed: the word I want to replace.

However, the copied text is still accessible on the kill ring. After the initial ctrl-y, meta-y will cycle through the kill ring's other (previous) selections. Its sort of difficult to describe; just give it a shot! It's become a huge timesaver for me.
