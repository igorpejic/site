---
author: "Igor Pejic"
date: 2018-03-15
linktitle: "It's time to stop using the mouse!"
title: "It's time to stop using the mouse!"
---
In this article, I will show you a way of thinking and working that will result in as much as a 20% increase in your productivity. Also, I will share with you the configuration I use to minimize mouse time, and some tricks I learned along the way.

## Why?

It started out as a joke in my teenage years when I used to claim that the best use for a mouse was to use it as a lasso for fetching things around me without having to stand up and stop coding.


In that spirit, the infamous quote that haunts me to this day, was coined: Why do you need a mouse while coding? You are not playing a FPS (first person shooting) game!

## The Big Debate: Who is Faster?

### In the beginning, there was Tog

Bruce "Tog" Tognazzini is an usability consultant famous for his controversial studies on the speed difference between mouse and keyboard usage. The studies were done as part of R & D on the Apple Human Interface with a reported cost of $50 million.

The summary can be found [here](https://www.asktog.com/TOI/toi06KeyboardVMouse1.html), and his conclusion is that for users who are new or inexperienced in a program interface, using the mouse is almost always faster. Another interesting fact is that the users who execute the same commands using the keyboard feel that they are faster but they are actually slower. This can be explained by analyzing what happens in the two opposing cases.

When the user uses the mouse to locate and click on an element, he doesn't need to engage any significant brainpower. Meanwhile, the keyboard user has to remember the right shortcut key combination to execute the same task.

This mental processing that takes place seems subjectively short to the keyboard user, although it is objectively slower than using the mouse. Tog explains that keyboard users experience actual amnesia, which makes them forget the amount of time they spent recollecting the shortcuts from memory.

However, Tog misses one critically important point: he analyzed users who were new to applications. For experienced users, for whom the commands are stored in what we often call muscle memory, using the keyboard is always faster than using the mouse.

This is exactly the case with developers: probably 90% of our work time is divided among using an editor, a browser, and the command line. This is a pretty big chunk of time spent in environments that are used repeatedly on a day to day basis (the same holds true for experienced designers who spend their days in Photoshop or engineers who "breathe" AutoCAD).

### Steep learning curve


It is true that the process of decreasing your "mouse-time" will make you slower at the start, but if you keep at it and learn all of the keyboard shortcuts and customize your configurations, you will reap exponential rewards your whole future career.

Various studies that analyze the prevention of RSI (repetitive strain injury) also recommend avoiding using the mouse as often as possible by using the function keys.

Not only will you be faster, but you are also protecting your health!

## My configuration

### The editor

It is not my intention to start an editor war in the comments, but I must say I am a proud user of Vim. Vim and Emacs were designed when using a mouse was not so common, because graphical interfaces were not yet so advanced.

The legacy of Vim and Emacs can be found in various programs on *nix operating systems which, for example, support hjkl movement inside previews or Emacs bindings inside search fields.

Considering that as a developer you will spend a lot of time in your editor, it is very wise to know the ins and outs of the features offered and the keyboard shortcuts that will speed up your execution.

Emacs, Vim, Sublime, Atom, Intel, JetBrains, Brackets, Notepad++, etc. are all valid choices that offer plentiful shortcuts and configuration options.

"Use a single editor well" is one of the tips offered in the great programming classic The Pragmatic Programmer: From Journeyman to Master, which offers valuable tips for aspiring developers of any experience level.

Mastering your editor will allow you to keep your hands at their most natural position, the keyboard, at all times.

Vim can easily be configured using the .vimrc file. You can see my .vimrc, including all of the configurations presented in this post [here](https://github.com/igorpejic/dotfiles/blob/master/.vimrc).

### Switching windows

Switching windows/workspaces is something that needs to be done and is actually done quite often. Using a mouse to do this could be disastrous for your productivity.

Your hand has to travel from your keyboard to the mouse and come back just to accomplish this simple motion. Most people do this with a combination of Tab, Shift + Tab or Alt + ~ depending on the OS used.

I personally use a window manager called i3, which is super easy to configure and very customizable. The idea behind a window manager is to utilize the working space of your monitor more effectively by opening new and managing existing windows in a variety of ways. It also supports moving between windows and workspaces by using keyboard shortcuts.

Adding these simple lines:

```
bindsym $mod+h focus left
bindsym $mod+j focus down
bindsym $mod+k focus up
bindsym $mod+l focus right
```

to my .i3/config allows me to move between windows using the configurable mod key, which is Caps Lock in my case, and the natural vim-like movement keys hjkl. Window managers also provide keyboard shortcuts for closing, opening, and resizing windows, all from the comfort of your keyboard.

### The shell

Using a good shell that you understand and can customize to your needs is essential if you are doing remote server administration or simply if you are used to working in the terminal rather than the GUI.

My favorite shell is the Z shell (Zsh) because of the amount of configuration options and plentitude of packages supported in the community-driven oh-my-zshrc.

If you are a frequent user of the shell, you are probably familiar with the feature of navigating the history of your commands, usually with the Up and Down arrow keys (this history can also probably be brought up if you just type `history` into your shell).

The default history retrieval is actually quite naïve and doesn't take into consideration the text that has been inputted before the Up and Down arrow keys are pressed.

Another possibility of navigating the history is using the Ctrl+R combination to enable reverse-search, which can be great if you remember exactly what a part of the command was, but you can run into problems if there are multiple commands containing the same search substring.

A great mentor of mine once showed me this trick I will share with you today: history search based on words inputted until that point.

Usually, this is done with arrow keys, but I have taken it a notch further because reaching for the arrow keys moves your right key from the neutral home row key position, so I remapped Ctrl+P for backward and Ctrl+N for forward search.


This magic is done by enabling the great history-substring-search plugin in your ~/.zshrc:

```
plugins=(history-substring-search)
```

and by mapping the great productivity enhancing Ctrl+P and Ctrl+N combination in ~/.oh-my-zsh/lib/key-bindings.zsh

```bash
if [[ "${terminfo[kcuu1]}" != "" ]]; then
  bindkey "^P" history-substring-search-up
fi
if [[ "${terminfo[kcud1]}" != "" ]]; then
  bindkey "^N" history-substring-search-down
fi
```

Another important thing to note about shell usage is that you should know some of the Emacs key-bindings that are enabled by default while you are typing. Here are some of the most common ones:

- `ctrl + a`: move cursor to first char  
- `ctrl + e`: move cursor to last char  
- `ctrl + u`: cut to the first char  
- `ctrl + k`: cut to the last char  
- `ctrl + y`: paste the clipboard of `ctrl + k` or `ctrl + u`  
- `ctrl + r`: history reverse search  
- `ctrl + l`: clear screen  
- `ctrl + w`: delete word to the left  
- `ctrl + t`: swap the last two chars and move cursor to the right  
- `ctrl + v + tab`: insert tab in shell  

- `alt + f`: move cursor to next word  
- `alt + b`: move cursor to previous word  
- `alt + .`: paste the last argument of the last entered command  

Note: in most shells, a Vim mode, instead of the Emacs one, can also be enabled, but I personally don't like it for editing commands that are usually quite short text (jumping in and out of the Vim insert mode seems too time consuming, and the Vim quick command in insert mode is not as powerful as the Emacs one).

### The browser

This is the step where most keyboard apologists (including me) occasionally fail and reach towards the mouse, but this is also the place where most of the improvements can be made.

For basic searching and navigating pages, I recommend the great plugin Vimium (for Chrome based browsers) or Tridactyl (for Firefox) which offer Vim-like behavior for the browser. If you would like to follow a link, you simply press F and each link gets a key combination attributed to it.

When the key combination is pressed, the link is followed, and you can continue navigating without the need to reach for the mouse.

Having said that, it is also worth noting that most very popular web applications, such as Gmail or Facebook offer integrated keyboard shortcuts that can be used without the need of plugins like Vimium. I recommend you learn those shortcuts if you spend a lot of time on those webpages or use plugins, such as the ones I recommended, as a one-for-all solution.

Until recently, I struggled with navigating the web console inside the browser, using only the keyboard because they didn't have a selection of keyboard shortcuts as rich as they have today.

Nowadays, both Firefox and Chromium offer a wide array of shortcuts and are constantly improving the developers' environments to make them more effective. We would only be foolish not to take advantage of that.

## Conclusion

We have covered the main areas of human-computer interaction a developer might and will face on a day to day basis, as well as how to optimize this process by increasing productivity, speed, and protecting your health.

Is this a final goodbye for the mouse? Of course not!

For some desktop applications that do not offer shortcuts, it is easier (and faster!) to use the mouse, and we should continue to do so.

What is important is that we are mindful at all times of what we are doing and how we are executing our actions. This process alone will create a snowball effect in which you too, little by little, will become a keyboard ninja!