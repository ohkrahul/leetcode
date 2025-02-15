# Find the Kth Largest Integer in the Array

## Problem Link
[LeetCode - Find the Kth Largest Integer in the Array](https://leetcode.com/problems/find-the-kth-largest-integer-in-the-array/)

## Difficulty
Medium

## Problem Description
<p>You are given an array of strings <code>nums</code> and an integer <code>k</code>. Each string in <code>nums</code> represents an integer without leading zeros.</p>

<p>Return <em>the string that represents the </em><code>k<sup>th</sup></code><em><strong> largest integer</strong> in </em><code>nums</code>.</p>

<p><strong>Note</strong>: Duplicate numbers should be counted distinctly. For example, if <code>nums</code> is <code>[&quot;1&quot;,&quot;2&quot;,&quot;2&quot;]</code>, <code>&quot;2&quot;</code> is the first largest integer, <code>&quot;2&quot;</code> is the second-largest integer, and <code>&quot;1&quot;</code> is the third-largest integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [&quot;3&quot;,&quot;6&quot;,&quot;7&quot;,&quot;10&quot;], k = 4
<strong>Output:</strong> &quot;3&quot;
<strong>Explanation:</strong>
The numbers in nums sorted in non-decreasing order are [&quot;3&quot;,&quot;6&quot;,&quot;7&quot;,&quot;10&quot;].
The 4<sup>th</sup> largest integer in nums is &quot;3&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [&quot;2&quot;,&quot;21&quot;,&quot;12&quot;,&quot;1&quot;], k = 3
<strong>Output:</strong> &quot;2&quot;
<strong>Explanation:</strong>
The numbers in nums sorted in non-decreasing order are [&quot;1&quot;,&quot;2&quot;,&quot;12&quot;,&quot;21&quot;].
The 3<sup>rd</sup> largest integer in nums is &quot;2&quot;.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [&quot;0&quot;,&quot;0&quot;], k = 2
<strong>Output:</strong> &quot;0&quot;
<strong>Explanation:</strong>
The numbers in nums sorted in non-decreasing order are [&quot;0&quot;,&quot;0&quot;].
The 2<sup>nd</sup> largest integer in nums is &quot;0&quot;.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= k &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= nums[i].length &lt;= 100</code></li>
	<li><code>nums[i]</code> consists of only digits.</li>
	<li><code>nums[i]</code> will not have any leading zeros.</li>
</ul>


## Test Cases
```
["3","6","7","10"]
4
["2","21","12","1"]
3
["0","0"]
2
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial thoughts:

   - This problem can be solved by sorting the array of strings and then returning the kth largest integer.
   - The time complexity of sorting is O(nlogn), where n is the length of the array.
   - We can also use a min-heap to solve this problem. The time complexity of building a min-heap is O(n), and the time complexity of popping the kth largest integer is O(klogn).

2. Solution Implementation:

```python
import heapq

class Solution:
    def findKthLargest(self, nums: List[str], k: int) -> str:
        # Convert the strings to integers and build a min-heap
        min_heap = []
        for num in nums:
            heapq.heappush(min_heap, int(num))

        # Pop the kth largest integer from the min-heap
        for _ in range(k - 1):
            heapq.heappop(min_heap)

        return str(heapq.heappop(min_heap))
```

3. Solution Explanation:

   - We first convert the strings in the array to integers and build a min-heap.
   - We then pop the kth largest integer from the min-heap.
   - The time complexity of this solution is O(nlogn), where n is the length of the array.
   - The space complexity of this solution is O(n), since we need to store the min-heap.

4. Complexity Analysis:

   - Time Complexity: O(nlogn)
   - Space Complexity: O(n)

## Topics
Array, String, Divide and Conquer, Sorting, Heap (Priority Queue), Quickselect

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-15
