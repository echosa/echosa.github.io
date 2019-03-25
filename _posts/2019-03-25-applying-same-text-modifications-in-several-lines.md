---
title: "ed Golf: Applying Same Text Modification in Several Lines"
date: 2019-03-25
categories: [blog]
tags: [ed]
---
Continuing with our ed golf exercises, today we tackle one that is more relevant to programming than the previous ones. We also have the first big mistake... fun! Let's jump into [Applying same text modification in several lines](http://www.vimgolf.com/challenges/5bbb82f969a25f0009541350)!

One note before we begin. I have changed the scoring system based on [this suggestion](https://twitter.com/tpenguinltg/status/1108688836958318592) on Twitter. Each session will now end with `wq`, which will be counted.

```
$ ed
### Insert start file
i
Assert.ThrowsAsync<Exception>(() => _auction.StartSellingItem());
Assert.ThrowsAsync<Exception>(() => _application.StartBiddingIn(_auction));
Assert.ThrowsAsync<Exception>(() => _auction.HasReceivedJoinRequestFromSniper());
Assert.ThrowsAsync<Exception>(() => _auction.AnnounceClosed());
Assert.ThrowsAsync<Exception>(() => _application.ShowsSniperHasLostAuction());
.
####################
### GOLF STARTS HERE
####################
### 14 - Remove everything that's not between _ and () [INCORRECT!]
g/_.*()/s//&;
Assert.ThrowsAsync<Exception>(() => _auction.StartSellingItem(););
Assert.ThrowsAsync<Exception>(() => _auction.HasReceivedJoinRequestFromSniper(););
Assert.ThrowsAsync<Exception>(() => _auction.AnnounceClosed(););
Assert.ThrowsAsync<Exception>(() => _application.ShowsSniperHasLostAuction(););
### 2 - Undo
u
### 21 - Remove everything that's not between _ and () [CLOSER, BUT STILL INCORRECT]
g/.*\(_.*\));/s//\1;
_auction.StartSellingItem();
_auction);
_auction.HasReceivedJoinRequestFromSniper();
_auction.AnnounceClosed();
_application.ShowsSniperHasLostAuction();
### 2 - Undo
u
### 22 - Remove the unwanted text from all lines
g/.* \(_.*\));/s//\1;
_auction.StartSellingItem();
_application.StartBiddingIn(_auction);
_auction.HasReceivedJoinRequestFromSniper();
_auction.AnnounceClosed();
_application.ShowsSniperHasLostAuction();
### 3 - Save and quit
wq
367
####################
### GOLF ENDS HERE - Total: 64 [HORRENDOUS!]
####################
### Output result
$ cat golf.txt 
_auction.StartSellingItem();
_application.StartBiddingIn(_auction);
_auction.HasReceivedJoinRequestFromSniper();
_auction.AnnounceClosed();
_application.ShowsSniperHasLostAuction();
```

Whew! Well, that could have gone better... 64. OUCH. Let's take a look at what went wrong. We learn from our mistakes, right?

As you can see, it took me three tries to get it right. The first time, I tried to use a new trick I learned from [this tweet](https://twitter.com/ed1conf/status/1107839605368385536) and [this tweet](https://twitter.com/tpenguinltg/status/1107841838143234049). `&` references the matched text in a substitution's search, so I figured I'd search for the text I want and substitute it back in. Obviously, that doesn't work because it doesn't address all the text I _don't_ want. Oops. 

Next, I did what I should have done, search for the lines with the part I want to keep in a sub-expression that I can replace back in, without the cruft, via `\1`. However, on the second line, the regular expression didn't do what I expected. The `_` matched with the second one on the line, not the first. I guess the regular expressions are not greedy by default. I thought they were. 

Finally, third time's the charm. In order to always match the correct `_`, I prepended a space to it in the regular expression. Success!

My score was terrible, but I learned a lot. Hopefully you did, too! I have to say, I like using the `g` (global) command for substitutions, since it outputs all the affected lines, instead of just the last affected line, like `s///g` does.

It shouldn't be too hard to beat my score this time. However, if you have any new tips or tricks to share for this one, please do so in the comments or [on Twitter](https://twitter.com/echosa).
