---
layout: post
title:  "[HOWTO] My own Linux installation guide"
date:   2016-02-27 17:43:29
categories: linux installation
---

Disklaimer:
It isn't ideal guide.
It's how I do things, then I need to set up my working environment
on a new machine.
I decided that I need something like this post, then I was in the middle
of installation of Arch Linux on [my new laptop][xps13].
Somehow it is my personal complement to [the beginners guide][arch-beginners].

### Arch Linux Installation

You need to start the installation from opening
the aforementioned [beginners guide][arch-beginners]. 
There are two official wiki pages to start from, then you are installing Arch Linux:

The first thing to install is [vim][vim] 

### Secure Boot
### Emacs
### Dropbox
### dotfiles
### udev rules for usb mounting
### wifi / dhcpcd tethering 
### zathura .config/zathurarc
### trackpadtoggle.sh
### .xinitrc

### Beeps after suspending

```bash
# rm /etc/pm/sleep.d/90alsa
```

[vim]:         http://vim.org
[xps13]:       http://wiki.archlinux.org/XPS_13_(2016)