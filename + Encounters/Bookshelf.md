up:: [[Home]] / [[Sources]] 

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
```dataview
TABLE WITHOUT ID
	status as Status,
	rows.file.link as Book
FROM  #source/book 
WHERE !contains(file.path, "Templates")
GROUP BY status
SORT status
```

## List of all books 

```dataview
TABLE WITHOUT ID
	status as Status,
	link(file.link, title) as Title,
	author as Author
FROM #source/book 
WHERE !contains(file.path, "Templates")
SORT status DESC, file.ctime ASC
```