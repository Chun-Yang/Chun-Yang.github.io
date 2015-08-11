---
layout: post
title:  "Use control-s to save in Vim"
date:   2015-08-10 20:30:00
categories: vim
---

# Context
mac

# Why you should do that
Save is one of most common task we do in vim or any text editor. Most people
use ```:w<ENTER>``` to save in normal mode (3 strokes).
Also when in insert mode, we have to escape ```jj```/```control-[```/```<ESC>```
into normal mode to save (about 4 strokes).

Most modern editors, E.G. *sublime*, provide ```command-s``` as a shortcut.
It is relatively consistant to use ```control-s``` in vim to save.

# How to do that

## vim
{% highlight vimscript %}
# ~/.vimrc
nnoremap <c-s> :w<CR> # normal mode: save
inoremap <c-s> <Esc>:w<CR>l # insert mode: escape to normal and save
vnoremap <c-s> <Esc>:w<CR> # insert mode: escape to normal and save
{% endhighlight %}

## zsh
[why](http://superuser.com/questions/385175/how-to-reclaim-s-in-zsh)
{% highlight bash %}
# enable control-s and control-q
stty start undef
stty stop undef
setopt noflowcontrol
{% endhighlight %}

## bash
[why](http://unix.stackexchange.com/questions/72086/ctrl-s-hang-terminal-emulator)
{% highlight bash %}
# enable control-s and control-q
stty -ixon
{% endhighlight %}
