---
title: "Clojure Greed Update: Static Typing!"
date: 2015-03-29
categories: [blog]
tags: [clojure]
---
Well, folks. This was long overdue, but I finally did it! My [clojure-greed](https://github.com/echosa/clojure-greed) project now has static typing thanks to [core.typed](http://typedclojure.org)!
<!--more-->
Using core.typed is an interesting experience, for sure. However, I've found that being able to have custom types (like "grid" for the game board, etc.) and then annotate functions with things like "take a grid and a direction the player should move and return the (updated) grid" is very helpful. It allows me to think more abstractly and to specifically mark that intention down. It also makes sure that my functions meet those intentions.

For what it's worth, that example annotation text would look something like this:

```
(ann-form update-player [Grid Direction -> Grid])
```

I should note that sometimes using core.typed means writing slightly less elegant and more verbose code than would normally be required. If you're looking through my source code and think "Why is he doing it that way?", chances are you've found a relic of core.typed.

Anyway, feel free to look at the code to see how it looks and works. I like it, and have been making sure to use core.typed in my other clojure project [zork-fortress](https://github.com/echosa/zork-fortress). The difference there is, instead of going back and adding typing to a finished projects, I'm actually using "Type-Driven Development", meaning I'm writing my annotations and custom types *first*, and then writing my functions to satisfy them. 

I'd be remiss if I didn't recognize Ambrose, creator of core.typed, in this article. He has always helped me with any questions, concerns, or confusion I've had concerning core.typed, whether I asked on Twitter or IRC. Thank you, Ambrose. Your help has been greatly appreciated.
