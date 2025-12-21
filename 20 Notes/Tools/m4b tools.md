---
created: 2025-12-21 06:31
modified: 2025-06-22T19:16:10-04:00
---
up:: [[Tools]]
[[books]] [[reading]]


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

### Misplaced chapters

In some cases there is a shift between the chapter mark and the real beginning of a chapter. m4b-tool could try to correct that by detecting silences and relocating the chapter to the nearest silence:

m4b-tool chapters --adjust-by-silence -o "data/destination-with-adjusted-chapters.m4b" "data/source-with-misplaced-chapters.m4b"

It won't work, if the shift is to large or if the chapters are strongly misplaced, but since everything is done automatically, it's worth a try, isn't it?


.
No chapters at all

If you have a well known audiobook, like Harry Potter and the Philosopher’s Stone, you might be lucky that it is on musicbrainz.

In this case m4b-tool can try to correct the chapter information using silence detection and the musicbrainz data.

Since this is not a trivial task and prone to error, m4b-tool offers some parameters to correct misplaced chapter positions manually.
A typical workflow
Getting the musicbrainz id

You have to find the exact musicbrainz id:

    An easy way to find the book is to use the authors name or the readers name to search for it
    Once you found the book of interest, click on the list entry to show further information
    To get the musicbrainz id, open the details page and find the MBID (e.g. 8669da33-bf9c-47fe-adc9-23798a37b096)

Example: https://musicbrainz.org/work/8669da33-bf9c-47fe-adc9-23798a37b096

MBID: 8669da33-bf9c-47fe-adc9-23798a37b096

Finding main chapters

After getting the MBID you should find the main chapter points (where the name of the current chapter name is read aloud by the author).

m4b-tool chapters --merge-similar --first-chapter-offset 4000 --last-chapter-offset 3500 -m 8669da33-bf9c-47fe-adc9-23798a37b096 "../data/harry-potter-1.m4b"

Explanation:

    --merge-similar: merges all similar chapters (e.g. The Boy Who Lived, Part 1 and The Boy Who Lived, Part 2 will be merged to The Boy Who Lived)
    --first-chapter-offset: creates an start offset chapter called Offset First Chapter with a length of 4 seconds for skipping intros (e.g. audible, etc.)
    --last-chapter-offset: creates an end offset chapter called Offset Last Chapter with a length of 3,5 seconds for skipping outros (e.g. audible, etc.)
    -m: MBID


### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```
