# Check If All 1's Are at Least Length K Places Away

## Problem Link
[LeetCode - Check If All 1's Are at Least Length K Places Away](https://leetcode.com/problems/check-if-all-1s-are-at-least-length-k-places-away/)

## Difficulty
Easy

## Problem Description
<p>Given an binary array <code>nums</code> and an integer <code>k</code>, return <code>true</code><em> if all </em><code>1</code><em>&#39;s are at least </em><code>k</code><em> places away from each other, otherwise return </em><code>false</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/04/15/sample_1_1791.png" style="width: 428px; height: 181px;" />
<pre>
<strong>Input:</strong> nums = [1,0,0,0,1,0,0,1], k = 2
<strong>Output:</strong> true
<strong>Explanation:</strong> Each of the 1s are at least 2 places away from each other.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/04/15/sample_2_1791.png" style="width: 320px; height: 173px;" />
<pre>
<strong>Input:</strong> nums = [1,0,0,1,0,1], k = 2
<strong>Output:</strong> false
<strong>Explanation:</strong> The second 1 and third 1 are only one apart from each other.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= k &lt;= nums.length</code></li>
	<li><code>nums[i]</code> is <code>0</code> or <code>1</code></li>
</ul>


## Test Cases
```
[1,0,0,0,1,0,0,1]
2
[1,0,0,1,0,1]
2
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts:

### Problem Analysis:
- The problem is to check if there are no adjacent 1's in the `nums` array, where the distance between adjacent elements is less than or equal to `k`.

### Key Observations:
- We can iterate through the array.
- If we encounter a 1, we can check if there is another 1 within the next `k` elements.
- If there is, then return false.

### Possible Approaches:
- Iterate through the array. For each 1, check if there is another 1 within the next `k` elements. If there is, then return false.

## Solution Implementation:
```python
def kLengthApart(nums, k):
  """
  :type nums: List[int]
  :type k: int
  :rtype: bool
  """
  last_one = -1

  for i in range(len(nums)):
    if nums[i] == 1:
      if i - last_one <= k:
        return False
      last_one = i

  return True
```

## Solution Explanation:
- The solution uses a simple iteration through the array.
- For each 1, it checks if there is another 1 within the next `k` elements.
- If there is, then it returns false.
- Otherwise, it keeps track of the last 1 encountered and continues the iteration.

## Complexity Analysis:
### Time Complexity: O(N)
- The solution iterates through the array once, so the time complexity is O(N), where N is the length of the array.

### Space Complexity: O(1)
- The solution uses a constant amount of space, so the space complexity is O(1).

## Topics
Array

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-30
