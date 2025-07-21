---
created: 2024-09-28 12:16
modified: 2025-06-15T18:42:51-04:00

---
tags:: [[git]]
## How To Work With Multiple Github Accounts on a single Machine

[https://gist.github.com/rahularity/86da20fe3858e6b311de068201d279e3](https://gist.github.com/rahularity/86da20fe3858e6b311de068201d279e3)

```jsx
ssh-keygen -t rsa -C "[linvivian61@gmail.com](<mailto:linvivian61@gmail.com>)" -f "github-vivian-personal"
ssh-keygen -t rsa -C "[linvivian61@gmail.com](<mailto:linvivian61@gmail.com>)" -f "github-vivian-personal"
```

```jsx
ssh-add -K ~/.ssh/github-vivian-personal
```

```jsx
ssh-add C:\\Users\\CZKZQ1\\.ssh\\github-vivian-personal
```

```jsx
clone the repo
git clone git@github.com-{your-username}:{owner-user-name}/{the-repo-name}.git
example to clone  add the vivian-personal
git@github.coml:VivianLin61/ui-animations.git
```

```jsx
git@github.com-vivian-personal:VivianLin61/ui-animations.git
```

```jsx
git config user.email "[linvivian61@gmail.com](<mailto:linvivian61@gmail.com>)"
git config [user.name](<http://user.name/>) "Vivian Lin"
```

```jsx
git remote add origin git@github.com-vivian-personal:vivian-personal
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
