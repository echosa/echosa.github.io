---
title: "Git, GPG, and IDE"
date: 2016-08-18
categories: [blog]
tags: 
- git
- gpg
---
Today, I discovered that `git` allows for signing commits and tags with `gpg`. Awesome. However, I've gotten rather used to using the git integration in IntelliJ's IDEA IDE, which is actually quite nice. In order to get the git/gpg stuff working, though, a few tweaks were required. I'm writing those here so I can remember them in the future.
<!--more-->
A quick overview of the problem and the solution. The issue is that when you tell git to sign commits or tags (either via a command line argument or git config change), gpg will require your passphrase for the key. Makes sense. If you're using git from the command line, there's no issue. However, since gpg defaults to a CLI prompt for the password, if you try to make a git commit from an external program (say, an IDE, like IntelliJ IDEA), you won't be prompted for a passphrase and the commit won't be made. The solution, then, is to get gpg to ask for the passphrase in a way compatible with external applications, beyond pure CLI usage.

Note: these instructions will be specific to OS X (soon to be macOS [again]).

Required installs (can be installed with [homebrew](http://brew.sh)): git, gpg, pinentry-mac

1. Create a new gpg key (or use an existing one), and configure git to use it. GitHub has [excellent documentation](https://help.github.com/articles/generating-a-gpg-key/) about how to do this.

2. Tell gpg to use a GUI program, not the terminal, to ask for passphrase when signing things by adding this to `~/.gnupg/gpg.conf`:

```
no-tty
use-agent
```

3. Tell gpg-agent to use the `pinentry-mac` program by adding this to `~/.gnupg/gpg-agent.conf` (you'll need to create the file if it doesn't exist):

```
pinentry-program /usr/local/bin/pinentry-mac
```

The pinentry-mac program exactly as it sounds: a pin entry program for Macs. This is the GUI program that will replace the default CLI passphrase prompt.

4. [Optional] If you don't want to have to tell git to sign every commit manually by using `git commit -S`, you can tell git to always sign. I've done so globally, but you could do so on a project-by-project basis:

```
git config --global commit.gpgsign true
```

Now, whenever you commit and have git sign with gpg, you'll be prompted with a GUI popup instead of gpg trying to ask for a password on the command-line. Added bonus: pinentry-mac allows you to check "Save in keychain" so you don't have to put in your passphrase every single time. *WARNING* Only select this option if your computer already has other security precautions, is not used by anyone else, and is safe and secure. Otherwise, anyone with access to your computer would be able to make commits signed by your key!

So, there you have it. That should be all that's requried to get git's gpg signing playing nice with external programs. 

One last thing: just so you know, GitHub now has [built-in GPG verification](https://github.com/blog/2144-gpg-signature-verification).
