---
created: 2024-03-30 16:44
modified: 2025-06-23T22:14:40-04:00
---
tags:: [[bash]] 
## Kill Ports


```
lsof -i:3000 | awk 'NR>1 {print $2}' | uniq | xargs -I {} kill -9 {}
lsof -i:4000 | awk 'NR>1 {print $2}' | uniq | xargs -I {} kill -9 {}
```
