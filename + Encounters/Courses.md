---
modified: 2025-06-16T09:33:15-04:00
---
up:: [[+ Home]] / [[Sources]] 

# 📚 Courses

```dataview
TABLE WITHOUT ID
	rows.file.link as Course,
	status as Status
FROM  #source/course  
WHERE !contains(file.path, "Templates")
GROUP BY status
SORT status DESC
```


**Complete these courses**

[https://ui.dev/](https://ui.dev/)

ByteGrad - Professional React & Next.js (next.js best practices)

Frontend.fyi framer motion course

Animations for the web course