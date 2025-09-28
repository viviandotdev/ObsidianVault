 
 up:: [[+ Home]] / [[Sources]] 

# 📚 My Bookshelf

```dataview
TABLE WITHOUT ID
	status as Status,
	rows.file.link as Book
FROM #source/book 
WHERE !contains(file.path, "Templates")
GROUP BY status
SORT status
```
