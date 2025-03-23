---
patterns:
  - Cyclic Sort
difficulty: Easy
ROI: Low
leetcode_url: https://leetcode.com/problems/find-the-missing-number/
modified: 2025-03-22T23:48:07-04:00
type: problem
---

# find-the-missing-number

<p>You are given an integer <code>first</code>, an integer <code>last</code>, and a list of numbers <code>nums</code>. <code>nums</code> contains <strong>every</strong> integer between <code>first</code> and <code>last</code> (both inclusive), <strong>except</strong> one random number which is <strong>missing</strong>. Return the missing <strong>number</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">first = 3, last = 9, nums = [3,7,4,5,9,6]</span></p>

<p><strong>Output:</strong> <span class="example-io">8</span></p>

<p><strong>Explanation:</strong>&nbsp;</p>

<p>The number between 3 and 9 which is missing from <code>nums</code> is 8.</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">first = 2, last = 2, nums = []</span></p>

<p><strong>Output:</strong> <span class="example-io">2</span></p>

<p><strong>Explanation:</strong>&nbsp;</p>

<p>The only number in the range is 2.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= first &lt; last&nbsp;&lt;= 100</code></li>
	<li><code>len(nums) == last - first</code></li>
	<li>The input is generated such that <code>nums</code> contains every integer between <code>first</code> and <code>last</code>, except one missing integer.</li>
</ul>

