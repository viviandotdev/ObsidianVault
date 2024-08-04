---
created: 2023-07-26 16:04 
modified: Wednesday 26th July 2023 16:04:02
alias: 
---
up:: 
tags:: #pattern/binary-search #leetcode/medium
related: 

## Find K Closest Elements
### Problem Link: [Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/)

### Explanation
![[10 Extras/Excalidraw/Find K Closest Elements|500]]
![[Screenshot 2023-07-26 at 4.16.51 PM.png|400]]

### Solution
```python
class Solution:

def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
	l, r = 0, len(arr) - k
	while l < r:
		m = l + (r - l) // 2
		#A[mid]----------- x ---- A[mid + l]
		if x - arr[m] > arr[m + k] - x:
			l = m + 1 #move right
		else:
			r = m
	return arr[l:l+k]
```

### Resources
- https://www.youtube.com/watch?v=bhPQq7vqLEA&t=617s

