# Find the N-th Value After K Seconds

## Problem Link
[LeetCode - Find the N-th Value After K Seconds](https://leetcode.com/problems/find-the-n-th-value-after-k-seconds/)

## Difficulty
Medium

## Problem Description
<p>You are given two integers <code>n</code> and <code>k</code>.</p>

<p>Initially, you start with an array <code>a</code> of <code>n</code> integers where <code>a[i] = 1</code> for all <code>0 &lt;= i &lt;= n - 1</code>. After each second, you simultaneously update each element to be the sum of all its preceding elements plus the element itself. For example, after one second, <code>a[0]</code> remains the same, <code>a[1]</code> becomes <code>a[0] + a[1]</code>, <code>a[2]</code> becomes <code>a[0] + a[1] + a[2]</code>, and so on.</p>

<p>Return the <strong>value</strong> of <code>a[n - 1]</code> after <code>k</code> seconds.</p>

<p>Since the answer may be very large, return it <strong>modulo</strong> <code>10<sup>9</sup> + 7</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">n = 4, k = 5</span></p>

<p><strong>Output:</strong> <span class="example-io">56</span></p>

<p><strong>Explanation:</strong></p>

<table border="1">
	<tbody>
		<tr>
			<th>Second</th>
			<th>State After</th>
		</tr>
		<tr>
			<td>0</td>
			<td>[1,1,1,1]</td>
		</tr>
		<tr>
			<td>1</td>
			<td>[1,2,3,4]</td>
		</tr>
		<tr>
			<td>2</td>
			<td>[1,3,6,10]</td>
		</tr>
		<tr>
			<td>3</td>
			<td>[1,4,10,20]</td>
		</tr>
		<tr>
			<td>4</td>
			<td>[1,5,15,35]</td>
		</tr>
		<tr>
			<td>5</td>
			<td>[1,6,21,56]</td>
		</tr>
	</tbody>
</table>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">n = 5, k = 3</span></p>

<p><strong>Output:</strong> <span class="example-io">35</span></p>

<p><strong>Explanation:</strong></p>

<table border="1">
	<tbody>
		<tr>
			<th>Second</th>
			<th>State After</th>
		</tr>
		<tr>
			<td>0</td>
			<td>[1,1,1,1,1]</td>
		</tr>
		<tr>
			<td>1</td>
			<td>[1,2,3,4,5]</td>
		</tr>
		<tr>
			<td>2</td>
			<td>[1,3,6,10,15]</td>
		</tr>
		<tr>
			<td>3</td>
			<td>[1,4,10,20,35]</td>
		</tr>
	</tbody>
</table>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n, k &lt;= 1000</code></li>
</ul>


## Test Cases
```
4
5
5
3
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:

   - The problem asks us to find the value of `a[n - 1]` after `k` seconds.
   - We start with an array of size `n` where each element is 1.
   - Every second, each element is updated to be the sum of all its preceding elements plus itself.
   - We notice that as we move from the first element to the last element in the array, the sum of preceding elements increases, and the new value of an element is the previous sum plus itself.

2. Solution Implementation:
```python
class Solution:
    def kthValue(self, n: int, k: int) -> int:
        sum = (1 + k) * k // 2 % (10 ** 9 + 7)
        return sum % (10 ** 9 + 7)
```

3. Solution Explanation:

   - We first calculate the sum of the first `k` positive integers using the formula `(1 + k) * k // 2`.
   - We then take the sum modulo `(10 ** 9 + 7)` to get the final answer.
   - This approach works because the sum of all preceding elements up to `a[n - 1]` is `(1 + k) * k // 2`.
   - The sum after `k` seconds is simply `(1 + k) * k // 2 % (10 ** 9 + 7)`.

4. Complexity Analysis:

   - Time complexity: O(1) - Constant time complexity since we only perform a few simple operations.
   - Space complexity: O(1) - Constant space complexity since we don't allocate any additional data structures.

## Topics
Array, Math, Simulation, Combinatorics, Prefix Sum

Solved on: 2024-11-11
