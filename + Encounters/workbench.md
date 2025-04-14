---
modified: 2025-04-14T09:32:34-04:00
---
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.


You may assume that each input would have exactly one solution, and you may not use the same element twice.

two pointer solution?

**sorted**
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].


**not sorted**
Input: nums = [3,2,4], target = 6
Output: [1,2]

brute for algorithm
(n2)
3 + 2 = 5, 3 + 4 = 7
2 + 3 = 5, 2 + 4 = 6
sum with everyone except itsself to find the sum

**not sorted**
cannot use binary search
cannot use to pointers left and right pointers
since this array is not sorted a hash table apprach is prefered
