---
modified: 2025-06-24T07:46:32-04:00
---
type:: #map/view 

Here are "best practices" for managing your PKM system. 

I’m caring too much about the record of keep and searching everything but that doesn’t not matter
Systems become crutches and override our own judgement of what actually helps what what just becomes system maintenance


**Inspirations**
- Building a second brain
- How To Take Smart Notes
- Linking Your Thinking
- [Why I create - John's Digital Galaxy 🌌](https://notes.johnmavrick.com/Why+I+create)
- [GitHub - lyz-code/best-of-digital-gardens: Ranked list of awesome digital gardens / second brains](https://github.com/lyz-code/best-of-digital-gardens?tab=readme-ov-file)

**Programming**
[TIL | Things I’ve learned and/or things I want to remember. Notes, links, advice, example code, etc.](https://jessesquires.github.io/TIL/)
Managing my PKM system
	- [[My PKM Folders|My PKM Folders]]
	- [[My PKM Tags|My PKM Tags]]

**How to take notes**
[[How I Take Smart Notes- Books]]
[[How I Take Smart Notes- Videos]]
[[How to Write Atomic Notes]]
[[How to Write an Mini Essay]]


Managing my PKM workflows ♽
	- [[My PKM Workflows]]


### Notes
```dataview
LIST
FROM "30 Notes" AND [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "Outbox")
WHERE !contains(file.name, "+ Home")
WHERE !contains(file.name, "Queue")

SORT file.link asc
```

### Sources
```dataview
LIST
FROM "20 Sources" AND [[#]]
and !outgoing([[#]])
WHERE !contains(file.name, "Outbox")
WHERE !contains(file.name, "+ Home")
WHERE !contains(file.name, "Queue")

SORT file.link asc
```