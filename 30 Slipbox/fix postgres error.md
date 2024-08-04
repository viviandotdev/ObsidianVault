---
created: 2024-06-14 14:52 
modified: Friday 14th June 2024 14:52:48
alias: 
---
up::  
type:: #postgresql 
links:: [postgresql - 5: Input/output error Error: Failure while executing; \`/bin/launchctl bootstrap gui/502 and FATAL: password authentication failed for user - Stack Overflow](https://stackoverflow.com/questions/69094757/5-input-output-error-error-failure-while-executing-bin-launchctl-bootstrap)
## fix postgres error

```'
cd /opt/homebrew/var/postgresql@14
rm postmaster.pid
brew services restart postgresql
```

### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



