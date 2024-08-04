---
created: 2023-10-30 20:44
modified: Monday 30th October 2023 20:44:53
alias:
---
up::
tags:: #git
related:: [[git]]
## delete all local git branches


```bash
git branch | grep -v "develop" | grep -v "master" | grep -v "main" | xargs git branch -D
```


### Resources
[bash - Delete all local git branches - Stack Overflow](https://stackoverflow.com/questions/10610327/delete-all-local-git-branches)
