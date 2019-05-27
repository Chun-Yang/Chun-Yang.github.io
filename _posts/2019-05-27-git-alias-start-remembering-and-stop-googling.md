---
layout: default
title:  Git ABC - Start remembering and stop googling
date:   2019-05-27
permalink: /git-alias-start-remembering-and-stop-googling/
cover_url: /assets/image/git.jpg
comments: true
---

I was once a Git googler (I mean I google Git a lot :P) until one day I sit down and decide to spend a bit of time remembing the most common commands. My approach was to develope an easy to understand framework and use systmatic alias to replace Git commands. Here I present you my Git ABC.

## Git ABC
There are three stages our code will go through in Git. I used A, B and C to represent them.

### Stage A
Unstaged changes and untracked files are in stage A. `git status` will show them in red.
![Stage A](https://trentyang.com/assets/image/git-a.png){:class="zoomable"}

### Stage B
Once we `git add -A`, changes will be moved to stage B. `git status` will show them in green.
In Git lingo, these changes are now 'staged'.
![Stage B](https://trentyang.com/assets/image/git-b.png){:class="zoomable"}

### Stage C
After we `git commit -m`, changes will be moved to stage C (commited stage).

## Alias
Not comes the fun part.
![Git ABC](https://trentyang.com/assets/image/git-abc.svg){:class="zoomable"}

### Move forward
We should already be familiar with `git add` and `git commit` so I choose the following aliases to move changes forward
- `alias ga='git add -A'` (Git Add) move changes from stage A to B
- `alias gc='git commit -m'` (Git Commit) move changes from stage B to C

### Move backward
I use `go` to undo changes. We can think of it as 'go away' :)
- `alias go='git checkout'` undo changes from A
- `alias gou='git clean -id'` (GO Untracked) remove un-tracked files from A
- `alias gob='git reset HEAD'` (GO from B) move changes from B to A
- `alias goc='git reset --soft HEAD~1'` (GO from C) move changes from C to B
- `alias gocc='git reset --hard HEAD~1'` (GO from C Confirm) remove the whole commit from C

### Check differences between stages
I use `gd` (Git Diff) to check difference.
- `alias gd='git diff'` Difference between A and B
- `alias gdbc='git diff --cached'` Difference between B and C
- `alias gdac='git diff HEAD'` Difference between A and C
- `alias gdc='git diff HEAD^ HEAD'` All changes from the last Commit

Here I listed all the aliases bellow so that you can copy and paste into your shell config files.
```
# move forward
alias ga='git add -A'
alias gc='git commit -m'

# move backward / undo
alias go='git checkout'
alias gou='git clean -id' # u means Untracked files
alias gob='git reset HEAD'
alias goc='git reset --soft HEAD~1'
alias gocc='git reset --hard HEAD~1' # c means Confirm

# check difference
alias gd='git diff'
alias gdbc='git diff --cached'
alias gdac='git diff HEAD'
alias gdc='git diff HEAD^ HEAD'
```

## Bonus aliases
Some of my fun aliases do not fit into the framework above so I lump them here :)
```
# status
alias gs='git status'

# log
alias gl='git log'
alias glo='git log --oneline --decorate'

# stash and apply
alias gst='git stash'
alias gap='git stash apply --index'

# rebase
alias gr='git rebase'
alias grm='git fetch origin master:master && git rebase master'
alias grs='git rebase --skip'
alias grc='git rebase --continue'
alias gri='git rebase -i master'
```

## Go above and beyound
At last I encourage you to create your own aliases for profit and fun :)
