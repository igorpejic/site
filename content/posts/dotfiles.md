---
author: "Igor Pejic"
date: 2024-03-09
linktitle: Tools I enjoy
title: Tools I enjoy
weight: 10
---

> Tools amplify your talent. The better your tools, and the better you know how to use them, the more productive you can be.

From: _The Pragmatic Programmer_ by Andy Hunt

Many years of professional software engineering have led to my opinionated list of tools and their configurations that are a daily driver to get things done.

## My Toolset

If I had to describe my toolset it would be:
- keyboard-oriented (see this [blog](https://www.codementor.io/@igorpejic/it-s-time-to-stop-using-the-mouse-hg895pcbh) for the **why**)
- Vim-centric (i.e. avoiding using arrow keys)
- terminal-heavy (preference in using "text" instead of GUI)
- Linux-based (Ubuntu usually)
- [i3](https://i3wm.org/)-dependent (for windows management)

## My Dotfiles

Dotfiles are configuration files for various programs usually stored in the `home` directory of the current user.
In Linux, hidden files are identified with a leading dot (`.`). Since the configuration files are usually hidden, they are nicknamed "dotfiles".

For an up to date list of tools and configuration files, see:
https://github.com/igorpejic/dotfiles


---

### Remapping Caps Lock to Windows (Mod) key {#xmodmap}

> I wish to arbitrarily remap keys to different functions at a low-level.

Touch-typing means fingers are on the home row most of the time.

Using i3 window manager, modifier key is a central key for navigating / executing.
For comfort, I rather have the modifier key be in their line than to have to move the pinkie south-east to press the windows key.

Therefore, disable Caps Lock and make it into the Windows key.

`.Xmodmap`
```bash
! maps caps lock into "WIN_KEY"
clear control
keycode 66 = Super_L
add control = Control_L Control_R
clear lock
```

and activate it with:
```
xmodmap ~/.Xmodmap
```

### Seamless switching between docked / mobile modes

> I wish plugging in monitors / keyboards to work out of the box.

When I plug in the laptop into a docking station, I wish the screens to automatically get set to the correct resolutions and position.
I also wish the keyboard layout to be [correctly configured](#xmodmap).

[Autorandr](https://github.com/phillipberndt/autorandr) is a great tool which can automatically select a display configuration based on the connected devices.

It also offers a `postswitch` event firing after the display get auto-changed, to which we can link the keyboard mapping changes:

`~/.config/autorandr/postswitch`

```bash
xmodmap ~/.Xmodmap
```
