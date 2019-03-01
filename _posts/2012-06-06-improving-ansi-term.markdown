---
title: "Improving ansi-term"
date: 2012-06-06
categories: [blog]
tags:
- emacs
---
I use ansi-term quite a bit. Why leave Emacs to have a terminal? However, there were a few issues I had with ansi-term that were quite annoying.
<!--more-->
However, because Emacs is awesome, the issues were pretty easily fixed.
First things first, I didn't like that running `exit` in my terminal left a useless buffer around. A little searching around online, and I found the following solution, using defadvice:

```cl
(defadvice term-sentinel (around my-advice-term-sentinel (proc msg))
  (if (memq (process-status proc) '(signal exit))
      (let ((buffer (process-buffer proc)))
        ad-do-it
        (kill-buffer buffer))
    ad-do-it))
(ad-activate 'term-sentinel)
```

This tells term (which is used by ansi-term) to kill the buffer after the terminal is exited. The original I found online also killed the frame, but I use one frame with multiple windows, so I removed that call.

Secondly, I always use bash. I don't need ansi-term to ask me which shell to use every time I invoke it. Once again, defadvice to the rescue. I wrote the following bit of advice that lets the user set the shell program to a variable, then advise ansi-term to always use that (and not ask). The defvar could just as easily be made a defcustom, and perhaps one day I'll do that. For now, though, this works for me.

```cl
(defvar my-term-shell "/bin/bash")
(defadvice ansi-term (before force-bash)
  (interactive (list my-term-shell)))
(ad-activate 'ansi-term)
```

Another issue I has was with the display of certain characters and control codes. The following hook sets the term to use UTF-8.

```cl
(defun my-term-use-utf8 ()
  (set-buffer-process-coding-system 'utf-8-unix 'utf-8-unix))
(add-hook 'term-exec-hook 'my-term-use-utf8)
```

Next, I wanted urls that show up in my terminal (via man pages, help, info, errors, etc) to be clickable. This was solved very easily by hooking `goto-address-mode` into ansi-term. To make add more hooks into ansi-term easier in the future, I defined my own hook function, currently with just `goto-address-mode`:

```cl
(defun my-term-hook ()
  (goto-address-mode))
```

Then added my hook to term-mode-hook:

```cl
(add-hook 'term-mode-hook 'my-term-hook)
```

After this, I realized that C-y doesn't work in ansi-term like you'd expect. It pastes into the buffer, sure, but the text doesn't get sent to the process. So if you copy a bash command, then C-y it into the buffer, nothing happens when you press enter (because, as far as ansi-term is concerned, no text was entered at the prompt). The following function will paste whatever is copied into ansi-term in such a way that the process can, well, process it:

```cl
(defun my-term-paste (&amp;optional string)
 (interactive)
 (process-send-string
  (get-buffer-process (current-buffer))
  (if string string (current-kill 0))))
```

Then I just add the binding to my hook from before, making it this:

```cl
(defun my-term-hook ()
  (goto-address-mode)
  (define-key term-raw-map "\C-y" 'my-term-paste))
```

Since I've already hooked it into 'term-mode-hook, there's no reason to do so again. Simply reevaluate the function.

Finally, I've recently been using the [solarized theme](http://ethanschoonover.com/solarized), both in Emacs and in my terminals. However, ansi-term wasn't quite playing well with this. The colors were wrong in ansi-term, even though they were right in the rest of Emacs. A friend and co-worker of mine wrote the following bit of elisp that, when added to the term-mode-hook, makes ansi-term use the right colors for solarized. *(Note that this is only needed if you use solarized and your ansi-term doesn't look right. Installing solarized, either in emacs or on your system, is beyond the scope of this post. However, I should mention that you can find it via M-x package-list-packages. The one you probably want is `color-theme-solarized`.) So, adding the elisp he wrote to my my-term-hook results in this:

```cl
(defun my-term-hook ()
  (goto-address-mode)
  (define-key term-raw-map "\C-y" 'my-term-paste)
  (let ((base03  "#002b36")
        (base02  "#073642")
        (base01  "#586e75")
        (base00  "#657b83")
        (base0   "#839496")
        (base1   "#93a1a1")
        (base2   "#eee8d5")
        (base3   "#fdf6e3")
        (yellow  "#b58900")
        (orange  "#cb4b16")
        (red     "#dc322f")
        (magenta "#d33682")
        (violet  "#6c71c4")
        (blue    "#268bd2")
        (cyan    "#2aa198")
        (green   "#859900"))
    (setq ansi-term-color-vector
          (vconcat `(unspecified ,base02 ,red ,green ,yellow ,blue
                                 ,magenta ,cyan ,base2)))))
```

Again, its already added to my term-mode-hook, so reevaluate and off we go.

So there you have it. With a little bit of elisp, ansi-term is much more streamlined (in my opinion) and better to work with. Hopefully this information will help others in the future.
