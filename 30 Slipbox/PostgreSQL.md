---
created: 2023-12-17 13:00
modified: Sunday 17th December 2023 13:01:08
alias:
---
up::  [[My Tools]]
tags:: #postgresql #database

## PostgreSQL
**error** [macos - Homebrew postgres broken - Stack Overflow](https://stackoverflow.com/questions/27700596/homebrew-postgres-broken)
```
Name          Status     User      File
postgresql@14 error  256 vivianlin ~/Library/LaunchAgents/homebrew.mxcl.postgresql@14.plist
```
**fixes**
```
rm -rf /usr/local/var/postgres
```



```
psql
```
**verify the table creation**
```
\l

\q 
```


```
\du
```