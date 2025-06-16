---
created: 2024-03-30 16:44
modified: 2025-06-16T07:02:03-04:00
alias: 
---
tags:: [[bash]]
## Kill Ports


```
lsof -i:3000 | awk 'NR>1 {print $2}' | uniq | xargs -I {} kill -9 {}
lsof -i:4000 | awk 'NR>1 {print $2}' | uniq | xargs -I {} kill -9 {}
```
