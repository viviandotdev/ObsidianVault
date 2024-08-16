---
created: 2024-07-29 14:21 
modified: Monday 29th July 2024 14:21:12
alias: 
---
up::  
type:: #note/atomic🌳 
links::
## Framer Motion

How does framer motion work?
How does animate presence work?
What are layout animations?

Layout changes
changes that affect neighboring elements
CSS transforms are fast because they do require changing neighboring elements

First, Last, Inverse, Play
Animate layout changes using fast css properties like transform
It inverts any layout changes done by the browser
1. First- mesaure the position before any layout changes
2. Last- measure position after the layout changes happen
3. 


- AnimatePresence is needed to wrap motion.div in order for exit animations to work
	- **delays** the the **unmounting** of the component until the **exit animation has completed**. lets framer motion know when to apply exit animations or else the component would just be removed instantly. 
- You can add a key to a element for react to know when to mount and unmount it
### Resources
[Inside Framer's Magic Motion](https://www.nan.fyi/magic-motion)

[Animating Radix Primitives with Framer Motion · OlegWock](https://sinja.io/blog/animating-radix-primitives-with-framer-motion)

### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



