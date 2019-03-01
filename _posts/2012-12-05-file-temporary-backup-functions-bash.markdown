---
title: "File Temporary Backup/Move Functions (bash)"
date: 2012-12-05
categories: [blog]
tags: 
- bash
---
A lot of the time, when I'm working in a bash terminal, I find myself needing to move a file out of the way temporarily.
<!--more-->
I found myself doing this over and over again:

```bash
$ mv my-file my-file.bak
```

Then if I wanted to put the file back:

```bash
$ mv my-file.bak my-file
```

Now, with tab completion, this was a fairly quick process, but I still got tired of the repetition. Therefore, I did what any programmer would do: I wrote a function to do it for me! (Well, technically *two* functions.) 

You'll find them below. Feel free to take them, use them, change them, and even make suggestions for improvements or alternatives.  To use them, simply call `bak` or `unbak` and give the file name. There is no check for proper arguments or anything. (I trust myself to use this function correctly.) This was just a quick hack to get the job done without taking to much time away from my real work.

```bash
bak () {
    mv $1 $1.bak
}

unbak () {
    length=$((${#1} - 4))
    mv $1 ${1:0:$length}
}
```
