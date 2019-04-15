---
title: "ed Golf: Letterbox"
date: 2019-04-15
categories: [blog]
tags: [ed]
---
Well, after a couple of weeks off, I'm back with another episode of ed Golf! Today, we're taking on a very interesting challenge, so let's try our hand at [Letterbox](http://www.vimgolf.com/challenges/5c7b244ae74665000c0598a9)!

A couple of notes, first. After some suggestions on Twitter, I'm making a couple of changes to how ed Golf is played. First, since Vimgolf requires saving and existing (`ZZ`), we should do the same with ed Golf, so we'll be ending with `wq` and adding 3 to the score. (Remember to count when you press return!)

Secondly, since we're saving and exiting, we need to work with an actual file rather than just the in-memory buffer. Therefore, instead of opening ed and adding the starting text, I'll be opening a file already populated with the start text. I'll still print it out at the start, for reference, though.

Third, because we're working with files and exiting, which counts towards the score, we're already out of ed by the time it comes to check our answer. I've decided to have a pre-populated file with the correct answer, similar to the starting text file, and I'll be using `diff` to check my answer against it. No output from `diff` means the files are the same.

With all that out of the way, let's take a look at what we're starting with:

```
$ cat start
abcdefg
```

And what we're trying to end up with:

```
$ cat end
a b c d e f g
b           f
c           e
d           d
e           c
f           b
g f e d c b a
```

Now let's give this a shot!

```
$ ed start
8
,p  
abcdefg
####################
GOLF STARTS HERE
####################
### 9 - Use `rev` command to get reverse copy of the string on the next line
r !rev %
rev start
8
### 4 - Duplicate first line
1t1
### 68 - Use regular express to get the correct letters on the correct lines
2s#\(.\)\(.\)\(.\)\(.\)\(.\)\(.\)\(.\)#\2\6\
\3\5\
\4\4\
\5\3\
\6\2
fb
### 19 - Add spaces to create the square shape
2,6s#\(.\)#\1     
#Spaces end here ^
f     b
### 15 - Add additional spaces between the characters
,s#\(.\)#\1 #g
### 7 - Delete trailing spaces
,s/ $/
g f e d c b a
### 3 - Save and quit
wq
98
####################
GOLF ENDS HERE - Total: 125
####################
$ diff start end
$
```

Oh, boy. That was a doozy! It's not a score I'm proud of, but what I am proud of is being able to complete the challenge at all! Let's break this one down a bit, since there's quite a bit to unpack here.

The first thing I did was run the contents of the file (just the starting text) through the `rev` command, reading the result into a new line in the file.. This is obviously system-specific, but ed is all about working with what you have on your system, right? ed edits text, and other programs do other things. The result of this command is that we end up with two lines, the starting one and the reverse:

```
abcdefg
gfedcba
```

Next, my idea was to have some text to work with, without touching the already correct first and last lines, so I duplicated the first line. Now I have:

```
abcdefg
abcedfg
gfedcba
```

Let's leave the first and last lines alone and just work with the second line. The next command is the big one. I use substitution to break apart the line and put the correct letters on the correct lines (no spaces yet). After this command, I have:

```
abcdefg
bf
ce
dd
ec
fb
gfedcba
```

Getting closer! Next, I add spaces to create the square shape, leaving me with:

```
abcdefg
b     f
c     e
d     d
e     c
f     b
gfedcba
```

So close, now! All we're missing is the space padding. After adding it, I have this (the `$` represents where the lines end):

```
a b c d e f g $
b           f $
c           e $
d           d $
e           c $
f           b $
g f e d c b a $
```

As you can see, we have trailing spaces that shouldn't be there, so I get rid of them before saving and exiting, leaving:

```
a b c d e f g$
b           f$
c           e$
d           d$
e           c$
f           b$
g f e d c b a$
```

Like I said before, I'm not particularly happy with this score. Let's see what we can shave off. The first thing I notice is that, in the big substitution, I don't actually need all the matches. Specifically, I don't need `a` (the first match) or `g` (the seventh and last match). So, we can lower our score with a slightly improved substitution command:

```
2s#.\(.\)\(.\)\(.\)\(.\)\(.\).#\1\5\
\2\4\
\3\3\
\4\2\
\5\1
```

Simply removing the matching from the first and last characters (i.e. replacing `\(.\)` with `.`) saves 8 characters, bringing the total down to 117. Still not great but better than before.

We can save even more by reducing the command to add the necessary spaces required to create the initial square shape. I keep forgetting to use `&` in substitutions ever since I learned about it recently, but let's use it here. An `&` in the replacement text is replaced with the entire matched text from the search part of the command. This means we don't have to use parentheses to get a match to put back in during replacement. Instead, we can do this:

```
2,6s/./&     #command ends here, with five trailing spaces
```

This saves another 5, giving us 112 now. We can save another 5 by doing the same with the command that adds the padding spaces:

```
,s/./& /g
```

That leaves us with a total improved score of 107, much better than the 125 we started with.

Can you do better? If so, let me know either in the comments or [on Twitter](https://twitter.com/echosa). Happy golfing!
