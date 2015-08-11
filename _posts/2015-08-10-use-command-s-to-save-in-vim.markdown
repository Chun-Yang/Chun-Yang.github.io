---
layout: post
title:  "Use control-s to save in Vim"
date:   2015-08-10 20:30:00
categories: vim
---

# Audience
This post is for **mac** user only

# Why you should do that
Save is one of most common task we do in vim or any text editor. Most people
use ```:w<ENTER>``` to save in normal mode (3 strokes).
Also when in insert mode, they have to escape using ```jj```, ```control-[```
or ```<ESC>``` into normal mode to save (about 4 strokes).
This is **NOT** efficient.

Most modern editors, like sublime, provide ```command-s``` as a shortcut.
It is relatively consistant to use ```control-s``` to save in vim.

# How to do that

- vim
{% highlight bash %}
# ~/.vimrc
nnoremap <c-s> :w<CR> # normal mode: save
inoremap <c-s> <Esc>:w<CR>l # insert mode: escape to normal and save
vnoremap <c-s> <Esc>:w<CR> # insert mode: escape to normal and save
{% endhighlight %}

- zsh (if you use)  
[why you need to do this][zsh]
{% highlight bash %}
# ~/.zshrc
# enable control-s and control-q
stty start undef
stty stop undef
setopt noflowcontrol
{% endhighlight %}

- bash (if you use)  
[why you need to do this][bash]
{% highlight bash %}
# ~/.bash_profile or ~/.bashrc
# enable control-s and control-q
stty -ixon
{% endhighlight %}

[zsh]: http://superuser.com/questions/385175/how-to-reclaim-s-in-zsh
[bash]: http://unix.stackexchange.com/questions/72086/ctrl-s-hang-terminal-emulator
