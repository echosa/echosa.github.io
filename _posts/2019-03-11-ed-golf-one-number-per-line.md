---
title: "ed Golf: One Number Per Line"
date: 2019-03-11
categories: [blog]
tags: [ed]
---
As I mentioned in my [last post]({{ site.baseurl }}{% post_url 2019-03-06-learning-and-using-the-standard-editor %}), I have been using the text editor ed for lots of things lately. In an effort to become more familiar with it and get some practice in, I have decided to try some [VimGolf](https://www.vimgolf.com) exercises in ed! I don't expect to beat the VimGolf scores. I do expect to learn more about ed, how to use it effectively, and try and see if I can find the minimum number of commands/keystrokes necessary for each exercise. So, without further ado, let's take a look at our first exercise: [One Number Per Line](https://www.vimgolf.com/challenges/56fb2e75ccffcc0009026473).

The exercise is pretty simple. Take a file that has comma-separated numbers and change it so that each number is on its own line. In these posts, I'll be posting commented ed sessions showing everything I've done between starting ed and getting the final result. For this challenge, here's what I did:

```
$ ed
### Input start file
i
- One number per line -
-----------------------
2,3,5,7,
11,13,17,
19,23,29,
.
####################
### GOLF STARTS HERE
####################
### 6 - Delete all lines without a comma
v/,/d
### 3 - Join all lines into one
,j
### 10 - Replace all commas with newlines
,s/,/\
/g
### 2 - Delete trailing empty line
d
####################
### GOLF ENDS HERE - Total: 21
####################
### Output result
,p
2
3
5
7
11
13
17
19
23
29
```

As you can see, my score was 21. Not bad! At least, I don't think so. However, I feel like there are some improvements that can be made, so let's explore.

The first command I ran, `v/,/d`, scored 6 (we can't forget to count pressing return/enter!). This command is what I used to get rid of the heading text by deleting all lines without commas. This works, of course, but we can do better. If we directly delete the heading text with `1,2d` (which deletes the first two lines), we can shave two points off of our score, giving us 19 instead.

I'm not able to see any other improvements, but I'm sure I'm missing something. If you see any ways to improve the score, let me know! Let's all learn together!
