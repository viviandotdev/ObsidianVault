---
modified: 2025-04-14T09:28:09-04:00
---
up:: [[leetcode]]

[Two Pointers in 7 minutes | LeetCode Pattern - YouTube](https://www.youtube.com/watch?v=QzZ7nmouLTI&list=PLK63NuByH5o-tqaMUHRA4r8ObRW7PWz45&index=1)
Iterate through an array or list looking for pairs of elements that meet a specific criteria

**Conditions**- Sorted arrays or lists where you need to find pairs that satisfy a specific condition
Sorted think of binary search
Linear data structures -> arrays, strings and linked lists
O(n^2) to O(n)

Words-
substring, contiguous, subarray


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
