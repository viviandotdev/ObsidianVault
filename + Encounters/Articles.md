ep:: [[Home]] / [[Sources]] 

## Articles

```dataview
TABLE WITHOUT ID
	status as Status,
	rows.file.link as Book
FROM  #source/article 
WHERE !contains(file.path, "Templates")
GROUP BY status
SORT raindrop_id ASC
SORT status

```
