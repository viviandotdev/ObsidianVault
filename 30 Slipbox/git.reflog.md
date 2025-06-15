---
created: 2023-11-03 18:41
modified: 2025-06-15T07:11:24-04:00
alias: 
---
type:: #note
tags:: [[git]]

## git.reflog

**Undo with:** `git reflog` and `git reset`

`git reflog` shows a list of times when `HEAD` changed

`HEAD` changes when you switch branches, make commits and un make commits,


`git reset --hard <SHA>`: restore the project’s history as it was at that moment in time use


`git checkout <SHA> -- <filename>`:  recreate one or more files in your working directory as they were at that moment in time, without altering history


`git cherry-pick <SHA>`: replay _exactly one_ of those commits into your repository use

### Resources
[How to undo (almost) anything with Git - The GitHub Blog](https://github.blog/2015-06-08-how-to-undo-almost-anything-with-git/)
