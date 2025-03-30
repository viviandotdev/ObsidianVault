observations what is the problem asking?

Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each unique element appears only **once**.

properties
-sorted array
-duplicates
-remove them so that that each unique element appears once
- return k which is the number of non dups in the array
- the array should maintain the order

two pointers
one that keeps track of the next non duplicate
then another to look for the element to place
slow -> nextNonDuplicate = 0
fast -> traverse the array to find the next value

nextNonDuplicate - 1 []
nums = [1,1,2]

