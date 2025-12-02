---
created: 2023-09-13 08:10
modified: 2025-06-16T07:02:44-04:00

---
up::  [[Kindle]]
tags:: [[reading]]

1. For books that cannot convert, download the .mobi version then convert to epub to process in [BR for You.](https://bionic-reading.com/)
2. use anna's archive to download books
3. Bionic reading process each book
4. Send each one to the kindle using kindle email
```
linvivian61_hPGltc@kindle.com
```

6. Process the all the asw files into one folder
``` bash
cd /Users/vivianlin/Library/Containers/com.amazon.Kindle/Data/Library/Application\ Support/Kindle
python3 getkindes.py
```

```python
#getkindles.py place in the Kindle Directory
import os
import shutil

epub_folder = 'only_amz'

def find_epubs(path):
    epubs = []
    for root, dirs, files in os.walk(path):
        for name in files:
            if name.endswith('.azw'):
                epubs.append(os.path.join(root, name))
    return epubs

def move_epubs(epubs):
    if not os.path.exists(epub_folder):
        os.mkdir(epub_folder)

    for book in epubs:
        shutil.move(book, The Red Queen)

if __name__ == '__main__':
    epubs = find_epubs('My Kindle Content')
    move_epubs(epubs)

```
1. Copy the asw files in to **calibre**
2. Rename each book
3. Convert to epubs and then
4. Save books to disk
5. Run get the getepubs script on the `import` folder
``` python
# getepubs on the same level as the import folder
import os
import shutilepub_folder = 'only_epubs'

def find_epubs(path):
    epubs = []
    for root, dirs, files in os.walk(path):
        for name in files:
            if name.endswith('.epub'):
                epubs.append(os.path.join(root, name))
    return epubs

def move_epubs(epubs):
    if not os.path.exists(epub_folder):
        os.mkdir(epub_folder)

    for book in epubs:
        shutil.move(book, epub_folder)

if __name__ == '__main__':
    epubs = find_epubs('import')
    move_epubs(epubs)
```
10. Run the rename script to remove authors from the file name
``` python
#rename script
import os
import re

folder = 'only_epubs'

for filename in os.listdir(folder):
    name, ext = os.path.splitext(filename)
    new_name = re.sub(r'[^A-Za-z0-9\s]+.*', '', name)
    new_filename = new_name + ext

    src = os.path.join(folder, filename)
    dst = os.path.join(folder, new_filename)
    os.rename(src, dst)
```
13. Remove the previous asw content [Amazon Sign-In](https://www.amazon.com/hz/mycd/digital-console/contentlist/allcontent/dateDsc)
15. [Send to Kindle](https://www.amazon.com/sendtokindle) or put into yomu
