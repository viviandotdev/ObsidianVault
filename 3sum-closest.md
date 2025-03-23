---
patterns: Two Pointers
difficulty: Medium
ROI: High
leetcode_url: https://leetcode.com/problems/3sum-closest/
modified: 2025-03-22T22:32:56-04:00
type: problem
---

# 3sum-closest

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. 

Return *the sum of the three integers*. 

You may assume that each input would have exactly one solution. 

**Example 1:**
<pre>
<strong>Input:</strong> nums = [-1,2,1,-4], target =1  
<b>Output:</b> 2  
<b>Explanation:</b> The sum that is closest to the target is 2. (-1 +2 +1 =2).  
</pre>


**Example 2:**
<pre>
<b>Input:</b> nums = [0,0,0], target = 1
<b>Output:</b> 0
<b>Explanation:</b> The sum that is closest to the target is 0. (0 + 0 + 0 = 0).
</pre>

**Constraints:**
- `3 <= nums.length <= 500`
- `-1000 <= nums[i] <= 1000`
- `-104 <= target <= 104`