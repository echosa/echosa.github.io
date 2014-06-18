---
layout: post
title: "Let's Try Acme: Ep. 1 - Hello, World"
date: 2014-06-18 09:02
comments: true
categories: 
- acme
---
After my [initial research](/blog/2014/06/18/lets-try-acme-ep-0-research/), it's time to give ol' Acme a try.
<!--more-->
First things first - I needed to install Acme. [Homebrew](http://brew.sh) made that quite easy.

```
$ brew install acme
```

Then running it was just as easy.

```
$ acme

ACME - the ACME Crossassembler for Multiple Environments
  Copyright (C) 1998-2006 Marco Baye
This is ACME, release 0.91 ("Gargravarr"), 26 Mar 2006
  Platform independent version.
Current maintainer Krzysztof Dabrowski aka BruSH/ElysiuM
ACME comes with ABSOLUTELY NO WARRANTY; for details read the help file.
  This is free software, and you are welcome to redistribute it under
  certain conditions; as outlined in the GNU General Public License.
Dedicated to the wisest being I ever had the pleasure of reading
  books of (currently spending some time dead for tax reasons).
The newest version can be found at the ACME homepage:
  http://home.pages.de/~mac_bacon/smorbrod/acme/

Usage: acme [OPTION...] [FILE]...
  -h, --help             show this help and exit.
  -f, --format FORMAT    select output format.
  -o, --outfile FILE     select output file.
  -l, --labeldump FILE   select label dump file.
      --setpc NUMBER     set program counter.
      --cpu CPU          select target processor.
      --initmem NUMBER   define 'empty' memory.
      --maxerrors NUMBER set number of errors before exiting.
      --maxdepth NUMBER  set recursion depth for macro calls and !src.
  -vDIGIT                set verbosity level.
  -V, --version          show version and exit.
```

Or maybe not. I turns out that this particular Acme is not the text editor I was looking for. A bit of digging around showed me where I'd gone wrong.

```
$ brew rm acme
$ brew install plan9port
```

Acme comes as part of the plan9port package. However, since this package installs a mostly completely Plan9 system (from what I can tell, anyway), it installs certain utilities that are common, like `ls`. In order to not stomp on your existing system, though, plan9port wraps it's version of these commands in it's own wrapper command `9`. Now, finally, I can open Acme!

```
$ 9 acme
```

Success! On top of it all, it has native OS X full screen support! Bonus!

Now I'm starting at the default Acme window. Time to play around. Middle-click on `New` to open a new window. Middle-click on `Del` to close it. Right click on a file to open it. Awesome. Acme seems to be working.

The real fun will continue in the [next episode](http://localhost:4000/blog/2014/06/18/lets-try-acme-ep-2-wat/).
