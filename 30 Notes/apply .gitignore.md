---
modified: 2025-07-23T09:48:03-04:00
---
tags::[[git]]
type:: #note/dev
source::[Just a moment...](https://stackoverflow.com/questions/19663093/apply-gitignore-on-an-existing-repository-already-tracking-large-number-of-file)

# apply .gitignore 
First of all, commit all pending changes.

Then run this command:
```
git rm -r --cached .
```
This removes everything from the index, then just run:

```
git add .
```

Commit it:

```
git commit -m ".gitignore is now working"
```