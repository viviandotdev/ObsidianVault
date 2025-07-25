---
modified: 2025-07-25T12:08:40-04:00
---
tags:: [[leetcode]]

[Two Pointers in 7 minutes | LeetCode Pattern - YouTube](https://www.youtube.com/watch?v=QzZ7nmouLTI&list=PLK63NuByH5o-tqaMUHRA4r8ObRW7PWz45&index=1)

**Properties of Two Pointers Problem**
- **Medium `n` ($10^3$ to $10^6$)
- **Input Format
	- Sorted Array
	- String (Palindromes)
	- Linked list (fast/slow)
- **Output Format**
	- Modified Array/String (in-place operations)
- **Keywords**
	- Palindrome
	- Sorted array
	- Target sum
	- Remove duplicates


**Two pointers- same direction**
[[remove-duplicates-from-sorted-array]]
```python
def two_pointers_same(arr):
    slow, fast = 0, 0
    while fast < len(arr):
        # Process current elements
        current = process(arr[slow], arr[fast])
        
        # Update pointers based on condition
        if condition(arr[slow], arr[fast]):
            slow += 1
        
        # Fast pointer always moves forward
        fast += 1

```

**Two pointers- opposite direction**
[[two-sum-ii-input-array-is-sorted]]
```python
def two_pointers_opposite(arr):
    left, right = 0, len(arr) - 1
    while left < right:
        # Process current elements
        current = process(arr[left], arr[right])
        
        # Update pointers based on condition
        if condition(arr[left], arr[right]):
            left += 1
        else:
            right -= 1

```
