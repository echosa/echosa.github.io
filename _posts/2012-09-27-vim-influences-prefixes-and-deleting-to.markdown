---
title: "Vim Influences: Prefixes and Deleting to End of Buffer"
date: 2012-09-27T07:46:00-07:00
tags:
- emacs
---
So, having used Vim for a while previously, there are some things that I learned or liked that have carried over into my Emacs usage, making it even better.
<!--more-->
For instance, the use of prefixes. In Vim, if you want to delete a line, you type `dd`. If you want to delete 3 lines, you type `3dd`. In Emacs, I used to either keep typing C-k over and over to delete multiple lines or I would select the region and delete it that way. These days, I've been doing things more the Vim way by, for instance, typing C-3 C-k to delete three lines.

Anyway, another thing I missed from Vim was `dG` which would delete from the cursor to the end of the file/buffer. However, this is Emacs, and writing my own was trivial:


```cl
(defun delete-to-end-of-buffer (add-to-kill-ring-p)
  "Deletes from point to end of buffer.
If prefix argument is given, kill the region, adding it to the kill ring."
  (interactive "P")
  (if add-to-kill-ring-p
      (kill-region (point) (point-max))
    (delete-region (point) (point-max))))
```

I bound this function to M-D. Basically, I can type M-D from anywhere in a buffer and the text from point to the end of the buffer is deleted. If, for some reason, I want to have that text added to the kill-ring (basically cut instead of just flat out deleted), I can supply a prefix (C-u M-D) then yank that text where I want it to go with C-y.
