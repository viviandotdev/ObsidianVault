---
created: 2024-03-30 16:44
modified: Saturday 30th March 2024 16:44:50
alias:
---
up::
tags:: #bash #commands
links::
## Kill Ports


```
lsof -i:3000 | awk 'NR>1 {print $2}' | uniq | xargs -I {} kill -9 {}
lsof -i:4000 | awk 'NR>1 {print $2}' | uniq | xargs -I {} kill -9 {}
```
