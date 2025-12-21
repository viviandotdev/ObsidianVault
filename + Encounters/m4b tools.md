---
created: 2025-12-21 06:31
modified: 2025-06-22T19:16:10-04:00
---
tags:: [[Tools]]

With m4b-tool you can merge a set of audio files to one single m4b audiobook file.


```
m4b-tool merge "data/my-audio-book" --output-file="data/my-audio-book.m4b"
```



This merges all Audio-Files in folder data/my-audio-book into my-audio-book.m4b, using the tag-title of every file for generating chapters.

If there is a file data/my-audio-book/cover.jpg (or cover.jpeg or cover.png), it will be used as cover for the resulting m4b file.


```
m4b-tool merge --help
```


```
m4b-tool chapters --adjust-by-silence -o "data/destination-with-adjusted-chapters.m4b" "data/source-with-misplaced-chapters.m4b"
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
