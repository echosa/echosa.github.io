---
title: "Robust Startup"
date: 2010-03-30
tags:
- emacs
---
I've spent quite a bit of time working on my start-up files for emacs. Maybe its my OCD, but I want them as clean as possible (using customize and the [ELPA](http://tromey.com/elpa/) helps) and I want as few annoyances as possible.
<!--more-->
One thing that really annoys me is when I take my .emacs to a different computer or emacs installation, emacs tends to complain about missing libraries and such. Then it just stops loading the rest of the .emacs file and often I'm stuck with default emacs, which defeats the purpose of me using the .emacs file at all. The way I see it, if a library doesn't load, go ahead and let me know, but continue on, because the next might load just fine!

That's why I wrote the following code:


```cl
(let ((invalid-packages '())
      (invalid-found nil))
  (dolist (package-to-load packages-to-load)
    (condition-case nil
        (progn
          (require (intern (car package-to-load)))
          (if (cdr package-to-load)
              (mapcar 'eval (cdr package-to-load))))
      (error
       (setq invalid-found t)
       (setq invalid-packages (push (car package-to-load) invalid-packages)))))
  (if invalid-found
      (progn
        (get-buffer-create "*invalid-packages*")
        (switch-to-buffer "*invalid-packages*")
        (let ((package-names ""))
          (dolist (package-name invalid-packages)
            (setq package-names (concat package-names package-name ", ")))
          (setq package-names (substring package-names 0 -2))
          (insert (concat "These packages were not loaded: " package-names "\n"))))))
```

I have this just before the Custom section of my .emacs file. This will take a variable called `packages-to-load` and load the libraries it references. It also will run any extra commands for a library (like turning on a mode). The defined variable looks something like this:


```cl
(setq packages-to-load
      '(("my-setup-emacs")
        ("my-funcs"
         (load-library "my-keymap"))
        ("hideshow")
        ("revive")
        ("uniquify")
        ("window-number")
        ("ido"
         (ido-mode)
         (icomplete-mode 99))
        ("smex-autoloads"
         (smex-initialize))
        ("org"
         (setq org-directory "~/Documents/org")
         (add-hook 'org-mode-hook
                   (lambda ()
                     (auto-fill-mode t))))))
```


Notice I'm loading several libraries (ido, smex, my own my-setup, etc) and that some of them after post-load configurations. Ido, for instance, gets turned on and icomplete-mode gets set to 99.

Now, so far nothing is different than the standard "require package, run config". However, the difference comes when a package fails to load or an initialization fails to execute. Instead of completely stopping the execution of .emacs, the emacs stores the name of the library in a variable, then if any libraries failed by the time execution is done, a buffer called *invalid-packages* is created to tell you which libraries did not load. This way, all possible libraries will load, even if one fails.

***

Another change I've made to my .emacs is setting the load path. Its easy enough to just set each directory and sub-directory, but I found this ugly and annoying, especially when I have to load, for instance, ~/.emacs.d/org/lisp and ~/.emacs.d/org/contrib/lisp. The following code lets me just add paths to (or remove paths from) a list that will be added to the load path (relative to the given elisp directory). It makes more sense when you see/use it:


```cl
; adds the elisp directories to the load path if they are existing directories
; and not already in the load path
(let ((el-dir (file-name-as-directory "~/.emacs.d"))
      (el-subdirs (list "jira"
                        "mmm-mode"
                        "org-6.34c/lisp"
                        "org-6.34c/contrib/lisp"
                        "php")))
  (setq load-path (cons el-dir load-path))
  (dolist (subdir el-subdirs)
    (setq dir-to-load (file-name-as-directory (concat el-dir subdir)))
    (if (file-directory-p dir-to-load)
        (unless (member dir-to-load load-path)
          (setq load-path (cons dir-to-load load-path))))))
```

Adding a sub-directory (for instance, ~/.emacs.d/mypackage) is as simple as adding "mypackage" to the el-subdirs list and executing the code. The code checks to make sure it doesn't place duplicates in the load-path, so running this several times will not infinitely increase the size of the load-path with paths that are already a part of the string. Also, this code checks to make sure that the sub-directory actually exists. If it doesn't , once again, emacs doesn't complain and stop executing, it just skips it and goes along its merry way.

I'm working on a nice way to be able to remove sub-directories from the list, execute the code, and have them removed from the load-path. I can think of a few ways, I just have to figure out which is most elegant.

***

A couple of other side notes:

I always have toolbars and scrollbars turned off. This can cause a problem when running emacs in a terminal. The following code takes care of that:


```cl
; get rid of scroll bars and menus
; check for each function because window-system doesn't seem to work in macosx
(if (fboundp 'toggle-scroll-bar)
    (toggle-scroll-bar nil))
(if (fboundp 'tool-bar-mode)
    (tool-bar-mode 0))
```

If you use ELPA like I do, they standard code they give you to place in .emacs references a particular file. If this file exists, once again, emacs complains. Wrapping this in a statement that checks for the existence of the file solves this:


```cl
(let ((elpa-dir "~/.emacs.d/elpa/package.el"))
  (if (file-exists-p elpa-dir)
      (when
          (load
           (expand-file-name "~/.emacs.d/elpa/package.el"))
        (package-initialize))))
```

Well, that all I've got for now. Stay tuned for more, and as always feel free to comment!
