---
created: 2023-07-11 18:24
modified: Tuesday 11th July 2023 18:24:35
 Vim
---
up::  [[My Tools]]

## Vim
****
[vi - How can I do a 'change word' in Vim using the current paste buffer? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/88714/how-can-i-do-a-change-word-in-vim-using-the-current-paste-buffer)
viwp

**Moving Around**

| Keys | Description                              |
| ---- | ---------------------------------------- |
| N h  | left (also: `<BS>`, or `<Left>` key)     |
| N l  | right (also: `<Space>` or `<Right>` key) |
| N }  | N paragraphs forward                     |
| N {  | N  paragraphs backward                   |
| : N  | move to line N                           |
| :+N  | go N lines forward                       |
| :-N  | go N line backward                       |
| gm   | move to middle of screen line            |
| N w    | move ahead N words                      |
| N W    | move ahead N whitespace-delimited word |
| N b    | move back N word                       |
| N B    | move back N whitespace-delimited word  |
| G    | go to end of file                        |
|  gg    |  move to frist line                                        |
**Copy Paste Delete Change**

| Keys | Description                                                                |
| ---- | -------------------------------------------------------------------------- |
| dd   | delete current line (and put them in the same buffer that yank would have) |
| yy   | yank (copy) the current line                                               |
| p    | paste after the current cursor position (or full line)                     |
| cw     |  change word

**Folding**

| Key | Description                     |
| --- | ------------------------------- |
| zo  | open one fold under the cursor  |
| zc  | close one fold under the cursor |
| zR  | open all folds                  |
| zM  | close all folds                  |
**Other**

| Keys | Description |
| ---- | ----------- |
| .-     |    repeat command - do cw, then go to another location in the file and do the change word there, too       |

## Resources
[Commands List · Issue #1 · aioutecism/amVim-for-VSCode · GitHub](https://github.com/aioutecism/amVim-for-VSCode/issues/1)
[mza's list of useful vim commands](https://www.phys.hawaii.edu/~mza/PC/vim.html)
