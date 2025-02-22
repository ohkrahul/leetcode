# Ways to Make a Fair Array

## Problem Link
[LeetCode - Ways to Make a Fair Array](https://leetcode.com/problems/ways-to-make-a-fair-array/)

## Difficulty
Medium

## Problem Description
<p>You are given an integer array&nbsp;<code>nums</code>. You can choose <strong>exactly one</strong> index (<strong>0-indexed</strong>) and remove the element. Notice that the index of the elements may change after the removal.</p>

<p>For example, if <code>nums = [6,1,7,4,1]</code>:</p>

<ul>
	<li>Choosing to remove index <code>1</code> results in <code>nums = [6,7,4,1]</code>.</li>
	<li>Choosing to remove index <code>2</code> results in <code>nums = [6,1,4,1]</code>.</li>
	<li>Choosing to remove index <code>4</code> results in <code>nums = [6,1,7,4]</code>.</li>
</ul>

<p>An array is <strong>fair</strong> if the sum of the odd-indexed values equals the sum of the even-indexed values.</p>

<p>Return the <em><strong>number</strong> of indices that you could choose such that after the removal, </em><code>nums</code><em> </em><em>is <strong>fair</strong>. </em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,1,6,4]
<strong>Output:</strong> 1
<strong>Explanation:</strong>
Remove index 0: [1,6,4] -&gt; Even sum: 1 + 4 = 5. Odd sum: 6. Not fair.
Remove index 1: [2,6,4] -&gt; Even sum: 2 + 4 = 6. Odd sum: 6. Fair.
Remove index 2: [2,1,4] -&gt; Even sum: 2 + 4 = 6. Odd sum: 1. Not fair.
Remove index 3: [2,1,6] -&gt; Even sum: 2 + 6 = 8. Odd sum: 1. Not fair.
There is 1 index that you can remove to make nums fair.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,1,1]
<strong>Output:</strong> 3
<strong>Explanation:</strong>&nbsp;You can remove any index and the remaining array is fair.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,3]
<strong>Output:</strong> 0
<strong>Explanation:</strong>&nbsp;You cannot make a fair array after removing any index.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
</ul>


## Test Cases
```
[2,1,6,4]
[1,1,1]
[1,2,3]
```

## Initial Template
```python
# Code template not available
```

## Solution
### 1. Initial Thoughts
 - The problem asks the number of ways to remove exactly one element from the array such that after the removal, the array becomes fair.
 - The array is fair if the sum of odd-indexed values equals the sum of even-indexed values.
 - Key observation: removing an element from the array affects only the sum of the odd-indexed and even-indexed values by at most 1.
 - Potential approach: For each index, calculate the sum of odd-indexed and even-indexed values after removing the element at that index. Check if the two sums are equal. If yes, increment a counter. Finally, return the counter.

### 2. Solution Implementation
```python
from typing import List

class Solution:
    def waysToMakeFair(self, nums: List[int]) -> int:
        # Calculate the sum of all elements
        total_sum = sum(nums)

        # Initialize the odd and even sums as the sum of all elements
        odd_sum = total_sum
        even_sum = total_sum

        # Iterate over the array
        result = 0
        for i, num in enumerate(nums):
            # Remove the current element from the odd and even sums
            odd_sum -= num
            even_sum -= num

            # Check if removing the current element would make the array fair
            if i % 2 == 0:
                # Current element is at even index
                if (total_sum - odd_sum) == odd_sum:
                    result += 1
            else:
                # Current element is at odd index
                if (total_sum - even_sum) == even_sum:
                    result += 1

            # Add the current element back to the odd and even sums
            odd_sum += num
            even_sum += num

        return result
```

### 3. Solution Explanation
 - The solution iterates over each element in the array.
 - For each element at index `i`, it calculates the sum of odd-indexed and even-indexed values after removing the element at that index.
 - If the two sums are equal, it increments a counter.
 - Finally, it returns the counter.

### 4. Complexity Analysis
 - Time complexity: O(n), where n is the length of the array. We iterate over each element in the array once.
 - Space complexity: O(1). We do not use any additional data structures that scale with the size of the input.

## Topics
Array, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-22
