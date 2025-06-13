---
created: 2023-07-17 12:32
modified: 2025-06-13T07:42:30-04:00
alias: 
---
up::
tags:: [[git]]
related:

# git rebase

The git rebase command allows you to easily modify the history of your branch or repository.

The main use case of rebase is to intergate the branch updates and the main. One way we usually do this is through a merge from the branch to the master.

As an alternative to merging, you can rebase the feature branch onto main branch. This moves entire feature branch to begin on the tip of the main branch.

update the **main** branch
```
git checkout main
git fetch origin
git rebase origin main
```

rebase the **feature** branch onto the **main** branch
```
git checkout feature
git rebase main
```

### Resources
https://docs.github.com/en/get-started/using-git/about-git-rebase
https://www.atlassian.com/git/tutorials/merging-vs-rebasing
