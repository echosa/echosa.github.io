---
title: "Some Improved Navigation"
date: 2009-05-26
categories: [blog]
tags: [emacs]
---
I've added some functions and keybindings to my .emacs file that make navigation quite a bit better for me.
<!--more-->
 Of course, you can bind them to whatever you like:

```cl
(global-set-key (kbd "C-v") 'my-scroll-up)
(global-set-key (kbd "M-v") 'my-scroll-down)
(global-set-key (kbd "M-n") 'scroll-up-without-moving-point)
(global-set-key (kbd "M-p") 'scroll-down-without-moving-point)
(global-set-key "\C-xp" 'other-window-backwards)
(global-set-key (kbd "C-o") 'open-new-line)
```

By default, scroll-up and scroll-down will not move to the bottom or top of the buffer if you are already on the last or first page. This adds that functionality:

```cl
(defun my-scroll-up ()
  "Scroll unless on last page of buffer, in which case go to end of buffer."
  (interactive)
  (condition-case nil
      (scroll-up)
    (error
     (goto-char (point-max)))))

(defun my-scroll-down ()
  "Scroll unless on first page of buffer, in which case go to beginning of buffer."
  (interactive)
  (condition-case nil
      (scroll-down)
    (error
     (goto-char (point-min)))))
```

Sometimes its nice to scroll without moving the cursor/point. This can be done easily, I just added it as a function to I could bind it. I realize I could add it as a lambda function directly in the global-set-key call, but I prefer to have it as a separate function.

```cl
(defun scroll-up-without-moving-point ()
  "Scroll up without moving the cursor/point."
  (interactive)
  (scroll-up 1))

(defun scroll-down-without-moving-point ()
  "Scroll down without moving the cursor/point."
  (interactive)
  (scroll-down 1))
```

other-window is nice, but only for going forwards. This is an easy function for binding going backwards with other-window:

```cl
(defun other-window-backwards ()
  "Move to the previous window."
  (interactive)
  (other-window -1))
```

As blasphemous as it might be, I like a little more "vi-like" functionality when I open a new line. Try open-line in the middle of a line, then try this one to get a feel for the differences. Got this one from [EmacsWiki](http://www.emacswiki.org/emacs/OpenNextLine):

```cl
(defun open-new-line (arg)
  "Move to the next line and then opens a line. See also `newline-and-indent'."
  (interactive "p")
  (beginning-of-line)
  (open-line arg)
  (when newline-and-indent
    (indent-according-to-mode)))
```
