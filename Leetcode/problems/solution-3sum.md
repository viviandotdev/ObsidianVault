---
patterns:
  - Two Pointers
difficulty: Medium
ROI: High
leetcode_url: https://leetcode.com/problems/3sum/
modified: 2025-03-23T12:58:55-04:00
type: solution
---

# 3sum

1. **make as many observations as you can**
Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` that sum to 0
No duplicate triplets and the triplets must be unique

Find triplets that sum to 0
return all multiple solutions
the triplets do not have to be contigious
- two pointers (left, right)
- return all possible solutions
- array is not sorted


2. summarize the problem
3. go through the example 
`nums = [-1,0,1,2,-1,-4]`
output = `[[-1,-1,2],[-1,0,1]]`

we can break this down to a k(sum)
if we find two sum we can find three sum
we want to converge to zero
-1 +.
