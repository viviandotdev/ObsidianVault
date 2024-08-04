---
created: 2024-05-02 12:26 
modified: Thursday 2nd May 2024 12:26:28
alias: 
---
up::  
type:: #css #flexbox 
links::
## Understanding the Basis of Flex

`flex-wrap` - determines whether the flex items should stay in one line or can wrap on to multiple lines when there isn't enough space in the flex container.
flex-basis -  specifies the **initial size** of those items **before any available space is distributed** according to the flex-grow and flex-shrink properties.


 if you want two items per row with a gap of 24px between them, you must ensure that the total width of **both items plus the gap does not exceed the container's width.**

 If you set basis to 50%, each item would take up half the container's width, leaving no room for the gap.



**Sources**