---
title: "RE Builder \"query replace this\""
date: 2012-06-26
categories: [blog]
tags:
- emacs
---
I use M-x re-builder a *lot*. Its an interactive regular expression builder that really helps build proper regexps and is an excellent learning tool.
<!--more-->
However, in using it, I found myself repeating a particular workflow:
- build regexp in re-builder
- copy it
- run query-replace-regexp
- paste regexp as the search
- type in the replacement
- press return and off you go

This was a lot of repeated work, so I wrote a function, which I bind to a key in reb-mode-map (C-c M-%, since plain old M-% is query-replace) which can be run in the re-builder buffer to automatically search the target buffer (the one that re-builder matches as you build) for the regexp you built, and replace it with a string, which is the only prompted argument of the function.

That may all sound complication, but its not. The workflow becomes:
- build regexp in re-builder
- run reb-query-this-regexp (C-c M-%)
- type in the replacement
- press return and off you go

Here is the code:

```cl
(defun reb-query-replace-this-regxp (replace)
  "Uses the regexp built with re-builder to query the target buffer.
This function must be run from within the re-builder buffer, not the target
buffer.

Argument REPLACE String used to replace the matched strings in the buffer.
 Subexpression references can be used (\1, \2, etc)."
  (interactive "sReplace with: ")
  (if (eq major-mode 'reb-mode)
      (let ((reg (reb-read-regexp)))
        (select-window reb-target-window)
        (save-excursion
          (beginning-of-buffer)
          (query-replace-regexp reg replace)))
    (message "Not in a re-builder buffer!")))

(define-key reb-mode-map "\C-c\M-%" 'reb-query-replace-this-regxp)
```
