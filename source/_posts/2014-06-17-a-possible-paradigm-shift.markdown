---
layout: post
title: "A Possible Paradigm Shift"
date: 2014-06-17 08:57
comments: true
categories: 
- emacs
---
Lately I've been experiencing a change in the way I look at, think about, and use Emacs.
<!--more -->
Emacs was always a one-stop shop for me. If I *could* do it in Emacs, I did. Email. Web browsing. Twitter. Listening to music. Games. Shells and terminals. Even [Google Maps](http://echosa.github.io/blog/2010/11/10/google-maps-in-emacs/). Of course, I did coding and actual text editing as well.

Well, a while back a gave ol' vim a shot. I like it. Quite a bit, actually. It is my second preferred editor, and I even use [evil-mode](https://gitorious.org/evil/pages/Home) in Emacs now. I learned a lot during my time with vim, and I have been applying lessons learned to my other work flows. It has created a dichotomy in me that I've been struggling back and forth with for a while now.

Vi(m)'s big motive, so to speak, is to do one thing and do it well. It accomplishes this. It's fast and efficient. Editing in Vim is fast and efficient. This is largely why I have adopted evil-mode. However, I found myself asking "where is X?", where X could be terminals, web browsers, etc. These things simply don't exist in Vim (and, really, rightfully shouldn't). Those things aren't part of the One Thing it does well. That forced me to outsource these things to other programs. Programs I already used, mind you. This was, as crazy as it seems, a revelation. If I'm going to have a terminal, a web browser, etc. open *anyway*, I may as well make use of them.

So, here I am, years into my Emacs experience, finding myself with, once again, a new look on all things Emacs. Emacs is a [hell of a text editor](http://echosa.github.io/blog/2009/09/25/oh-yeah-its-text-editor/). It does lots of other things as well, some of which it does [extremely well](https://github.com/magit/magit). However, not *everything* needs to be done, or *should* be done, in Emacs. It hurts me just a little to say that, but I'm increasingly believing that to be true. Heresy, thy name is me.

I'd be remiss if I didn't mention another potential factor in this recent change of mind and heart. I'm slowly (but not *that* slowly) severing ties with the Google Machine. In doing so, I've become aware of just how tied in I was. It was eye opening and scary. Having all your eggs in one basket, so to speak, has its benefits, but also can basically be a self-imposed lock down.

As I was untangling myself from this web (heh... *get it?*), I began recognizing other similar situations I was in. Emacs was at the forefront. Being so tied in to Emacs, when it crashed (which, to be fair, is rare), an update went badly, or anything else prevented Emacs from working appropriately, it was detrimental. Spreading tasks to the appropriate *separate* handlers is important. This is the same reason why micro-frameworks have become a huge deal, especially in the PHP world. It's piecing together your own solutions with several parts that each do one thing and do it well.

The end result of all this is I'm going to use Emacs for what it's good for: development and text editing. This includes things like running terminals for tests or other things, using version control (seriously, magit is the shit [technical term]), and other development and text editing related things. Other tasks will be delegated elsewhere, including [2048](https://github.com/sprang/emacs-2048).

If you go through the history of Emacs posts on this blog, you'll see that I've flip-flopped on several topics and not kept up with various changes I've made (*cough* org-mode *cough*). This may very well fall into that category as well, and I may find myself back to doing as much in Emacs as possible. For now, though, I'll be spreading my work across multiple applications.
<hr />
Side notes:

You'll notice the title of this article says "possible". That's largely due to what I said in the last paragraph.

Also, as far as getting myself away from the Google Machine, to be fair, I've basically just jumped ship to Apple (for most, but not all, things). This may sound hypocritical, but a.) as I'm basically all Apple hardware these days anyway, it at least makes more sense than being tied into Google, and b.) Apple is now at least on par with Google [as far as the EFF is concerned](http://9to5mac.com/2014/05/15/eff-marks-apples-remarkable-improvement-in-protecting-customer-data-from-governments/). I'm not a complete hypocrite, though, as I've been looking at what Apple services I can move to other providers, so I'm at least trying to apply this same separation of services thought to my Apple tie-ins as well.
