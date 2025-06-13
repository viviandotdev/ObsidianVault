---
created: 2023-10-30 20:44
modified: 2025-06-13T07:48:06-04:00
alias: 
---
up::
related:: [[git]]
## delete all local git branches


```bash
git branch | grep -v "develop" | grep -v "master" | grep -v "main" | xargs git branch -D
```


### Resources
[bash - Delete all local git branches - Stack Overflow](https://stackoverflow.com/questions/10610327/delete-all-local-git-branches)
