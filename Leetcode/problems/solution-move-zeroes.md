---
patterns:
  - Arrays
  - Two Pointers
difficulty: Easy
ROI: High
leetcode_url: https://leetcode.com/problems/move-zeroes/
modified: 2025-04-14T11:33:56-04:00
type: solution
---

# move-zeroes
**problem:** [[move-zeroes]]
**edge case**

nums = [1]

Expected = [1]
Output =[0] is the 
**incrroect**
```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        #move all non zeros to the front
        nonZero = 0 #where to place the frist non zero
        for i in range(1, len(nums)): #this is incorrect should start at 0

            if nums[i] != 0:
                nums[nonZero] = nums[i]
                nonZero += 1 
            

        for i in range(nonZero, len(nums)):
            nums[i] = 0
```