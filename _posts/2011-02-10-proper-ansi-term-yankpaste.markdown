---
title: "Proper (Ansi-)Term Yank/Paste"
date: 2011-02-10T17:49:00-08:00
tags:
- emacs
- terminal
---
So, I've found myself using ansi-term quite a bit, including to run finch for my instant messaging needs. However, there's one main issue with which I found myself becoming frustrated: yanking (aka pasting).
<!--more-->
Ansi-term has two "mode": line and char. One acts as a terminal would (e.g. the up arrow will scroll through the output, as in scrolling through a call to `less`), and the other acts as an emacs buffer. The default is to be in the former, which sort of traps the cursor (mostly correctly), since no raw cursor movement commands are sent to the terminal just because you click elsewhere in the buffer.

This becomes mostly frustrating because it keeps yank from working properly. For example, if I wish to copy/paste a url into an instant message to a friend using finch inside ansi-term, the paste part doesn't work unless I enter the second ansi-term "mode". However, this makes the buffer not treat anything as special (i.e. window bounds, text areas, etc) and can wreak havoc on the message I'm trying to send.

For this reason, I wrote a quick little function that allows me to yank text into a terminal properly without switch modes. I present to you, my-term-paste:

```cl
(defun my-term-paste (&optional string)
  (interactive)
  (process-send-string
   (get-buffer-process (current-buffer))
   (if string string (current-kill 0))))
```

Basically all this does is send the current copied text (current-kill 0) to the terminal using process-send-string which sends it as raw terminal input, as if I had manually typed each letter. The result? I can copy some text, for instance a url from Chrome, then focus my ansi-term and run (my-term-paste) to paste the copied text properly into the buffer. Very handy for those who use terminal modes in emacs.
