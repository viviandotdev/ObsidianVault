---
patterns:
  - Arrays
  - Two Pointers
difficulty: Easy
ROI: High
leetcode_url: https://leetcode.com/problems/remove-duplicates-from-sorted-array/
modified: 2025-03-23T08:52:24-04:00
type: solution
---

# remove-duplicates-from-sorted-array

Pointers type - Fast and slow pointers

Given an integer array `nums` sorted in **non-decreasing order** 
Remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each unique element appears only **once**.
- sorted array (two pointer?)
- remove duplicates (keep track of count??)
	- since the array is sorted, we can use the previous pointer to find duplicates because duplicates will all be next to each other
The **relative order** of the elements should be kept the **same**.
- how to keep relative order the same?
	- if we see a duplicate keep the pointer at the same place and replace it until we find a non duplicate
what are the two pointers? slow and fast pointer
they start at i(0) and i + 1  (1)
**slow pointer** -> pointer for placing the next (non-duplicate number) next unique number (i + 1)
	first next non duplicate
**fast pointer** -> pointer for iterating the array to find the number that can replace next non-duplicate number (0)

			
Then return _the number of unique elements in_ `nums`.
- k = number of unique elements in nums, 

**Summary**
Change the array so duplicates are removed and that the first k elements are unique (no - dups) and maintain the order they appear in the array
The remaining elements can be anything

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        next_non_duplicate = 1

        i = 0
        while(i < len(nums)):
            if nums[next_non_duplicate - 1] != nums[i]:
                nums[next_non_duplicate] = nums[i]
                next_non_duplicate += 1
            i += 1

        return next_non_duplicate
```
[Remove Duplicates from Sorted Array - LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/submissions/1141600456/)

