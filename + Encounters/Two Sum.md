---
modified: 2025-02-27T08:56:37-05:00
---
Given array of `nums` return the indices of the two numbers such that they add up to `target`.

**Summary**
Given an array of integers find the two indices, where the values at the indices sum to the target

**Can we assume that they are sorted?**

nums = [2,7,11,15]
target = 9
0, 1 since nums[0] = 2 and nums[1] = 7
and 2 + 7 = 9

Sliding window technique
2 + 15 if greater than target decrement right
2 + 11 greater than target decrement right
2 + 9 greater than target r -= 1
2 + 7 == target return nums[index of 2 ] and nums [index of 7]
**make sense try an example where less than target**

nums = [2,3,6,9,10 11]
target = 16
2 + 11 is smaller left increment
3 + 11 = 14 smaller left increment
6 + 11 = 17 greater right decrement
6 + 10 = 16 target found

nums[l] + nums[r] if sum > target then r -= 1
nums[l] + nums[r] if sum < target then l += 1
if sum == target then return `l` and `r`

**solution works only if they are sorted**

```python 
class Solution:

def twoSum(self, nums: List[int], target: int) -> List[int]:



```