two sum input array is sorted
array

sorted

find two numbers whose sum adds up to specific target number

array 
sorted

two pointers
left and right pointer
two conditions
left + right pointer = two sum
if twoSum > targetSum:
	right -= 1 **need to make smaller**
elif twoSum < targetSum:
	left += 1 **need to make the sum larger**
left must be  < right
```
def twoSum(nums):
	left = 0
	right = len(nums) - 1
	while left < right:
		twoSum = left + right
		if (twoSum > target):
			right -= 1
		elif (twoSum < target):
			left += 1
		else:
			return [left, right]
```