# Find the Score of All Prefixes of an Array

## Problem Link
[LeetCode - Find the Score of All Prefixes of an Array](https://leetcode.com/problems/find-the-score-of-all-prefixes-of-an-array/)

## Difficulty
Medium

## Problem Description
<p>We define the <strong>conversion array</strong> <code>conver</code> of an array <code>arr</code> as follows:</p>

<ul>
	<li><code>conver[i] = arr[i] + max(arr[0..i])</code> where <code>max(arr[0..i])</code> is the maximum value of <code>arr[j]</code> over <code>0 &lt;= j &lt;= i</code>.</li>
</ul>

<p>We also define the <strong>score</strong> of an array <code>arr</code> as the sum of the values of the conversion array of <code>arr</code>.</p>

<p>Given a <strong>0-indexed</strong> integer array <code>nums</code> of length <code>n</code>, return <em>an array </em><code>ans</code><em> of length </em><code>n</code><em> where </em><code>ans[i]</code><em> is the score of the prefix</em> <code>nums[0..i]</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,3,7,5,10]
<strong>Output:</strong> [4,10,24,36,56]
<strong>Explanation:</strong> 
For the prefix [2], the conversion array is [4] hence the score is 4
For the prefix [2, 3], the conversion array is [4, 6] hence the score is 10
For the prefix [2, 3, 7], the conversion array is [4, 6, 14] hence the score is 24
For the prefix [2, 3, 7, 5], the conversion array is [4, 6, 14, 12] hence the score is 36
For the prefix [2, 3, 7, 5, 10], the conversion array is [4, 6, 14, 12, 20] hence the score is 56
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,1,2,4,8,16]
<strong>Output:</strong> [2,4,8,16,32,64]
<strong>Explanation:</strong> 
For the prefix [1], the conversion array is [2] hence the score is 2
For the prefix [1, 1], the conversion array is [2, 2] hence the score is 4
For the prefix [1, 1, 2], the conversion array is [2, 2, 4] hence the score is 8
For the prefix [1, 1, 2, 4], the conversion array is [2, 2, 4, 8] hence the score is 16
For the prefix [1, 1, 2, 4, 8], the conversion array is [2, 2, 4, 8, 16] hence the score is 32
For the prefix [1, 1, 2, 4, 8, 16], the conversion array is [2, 2, 4, 8, 16, 32] hence the score is 64
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
</ul>


## Test Cases
```
[2,3,7,5,10]
[1,1,2,4,8,16]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

- **Problem analysis:**
   - We have to find the score of all prefixes of a given array.
   - The score of the prefix is defined as the sum of the "conver" array which is nothing but the prefix sum of the original array with the running maximum.

- **Key observations:**
    - We can use prefix sum to calculate the prefix sum of the original array.
    - We can find the running maximum by maintaining the previous maximum as we iterate.
    - We can calculate the conver array by adding the running maximum to each prefix sum.
    - The score is the sum of the conver array.

- **Possible approaches:**
    - **Prefix Sum Approach:**
        - Precalculate the prefix sum of the original array.
        - Maintain a running maximum as we iterate to find the running maximum.
        - Calculate the conver array by adding the running maximum to each prefix sum.
        - Calculate the score as the sum of the conver array.
     - **TLE Approach:**
        - We can brute-force find the maximum for each prefix and then add it to the prefix sum. This approach will result in TLE.

2. **Solution Implementation:**
```python
def getMaximumScore(nums):
    """
    :type nums: List[int]
    :rtype: List[int]
    """
    n = len(nums)
    # Precalculate prefix sum of the original array
    prefix_sum = [0] * n
    prefix_sum[0] = nums[0]
    for i in range(1, n):
        prefix_sum[i] = prefix_sum[i - 1] + nums[i]

    # Maintain running maximum
    running_max = nums[0]

    # Initialize conver array and score array
    conver = [0] * n
    score = [0] * n

    for i in range(n):
        # Calculate conver array by adding running maximum to prefix sum
        conver[i] = prefix_sum[i] + running_max

        # Update running maximum
        running_max = max(running_max, nums[i])

        # Calculate score as sum of conver array
        score[i] = sum(conver)

    return score
```

3. **Solution Explanation:**

- We first precalculate the prefix sum of the original array.
- We maintain running maximum as we iterate to find the running maximum.
- We calculate the conver array by adding the running maximum to each prefix sum.
- We calculate the score as the sum of the conver array.
- We return the score of all prefixes.

4. **Complexity Analysis:**

- **Time complexity:** O(N)
   - We iterate through the array twice: once to precalculate the prefix sum and once to calculate the score.
- **Space complexity:** O(N)
   - we use an array to store the prefix sum, conver array, and score.

## Topics
Array, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-19
