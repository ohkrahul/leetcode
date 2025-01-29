# Count Good Triplets

## Problem Link
[LeetCode - Count Good Triplets](https://leetcode.com/problems/count-good-triplets/)

## Difficulty
Easy

## Problem Description
<p>Given an array of integers <code>arr</code>, and three integers&nbsp;<code>a</code>,&nbsp;<code>b</code>&nbsp;and&nbsp;<code>c</code>. You need to find the number of good triplets.</p>

<p>A triplet <code>(arr[i], arr[j], arr[k])</code>&nbsp;is <strong>good</strong> if the following conditions are true:</p>

<ul>
	<li><code>0 &lt;= i &lt; j &lt; k &lt;&nbsp;arr.length</code></li>
	<li><code>|arr[i] - arr[j]| &lt;= a</code></li>
	<li><code>|arr[j] - arr[k]| &lt;= b</code></li>
	<li><code>|arr[i] - arr[k]| &lt;= c</code></li>
</ul>

<p>Where <code>|x|</code> denotes the absolute value of <code>x</code>.</p>

<p>Return<em> the number of good triplets</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> arr = [3,0,1,1,9,7], a = 7, b = 2, c = 3
<strong>Output:</strong> 4
<strong>Explanation:</strong>&nbsp;There are 4 good triplets: [(3,0,1), (3,0,1), (3,1,1), (0,1,1)].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> arr = [1,1,2,2,3], a = 0, b = 0, c = 1
<strong>Output:</strong> 0
<strong>Explanation: </strong>No triplet satisfies all conditions.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= arr.length &lt;= 100</code></li>
	<li><code>0 &lt;= arr[i] &lt;= 1000</code></li>
	<li><code>0 &lt;= a, b, c &lt;= 1000</code></li>
</ul>

## Test Cases
```
[3,0,1,1,9,7]
7
2
3
[1,1,2,2,3]
0
0
1
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts:

- This problem can be solved with a brute force approach. We can iterate over all possible triplets in the array, and check if they satisfy the given conditions. The time complexity of this approach would be O(`n^3`), where `n` is the length of the array.
- Another approach is to sort the array, and then iterate over all possible pairs of elements. For each pair, we can check if there exists an element in the array that satisfies the given conditions. The time complexity of this approach would be O(`n^2logn`), where `n` is the length of the array.

## 2. Solution Implementation:
```python
def countGoodTriplets(arr, a, b, c):
    """
    :type arr: List[int]
    :type a: int
    :type b: int
    :type c: int
    :rtype: int
    """
    arr.sort()
    count = 0

    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if abs(arr[j] - arr[i]) <= a:
                l, r = j + 1, len(arr) - 1
                while l <= r:
                    mid = (l + r) // 2
                    if abs(arr[mid] - arr[j]) <= b:
                        if abs(arr[mid] - arr[i]) <= c:
                            count += r - mid + 1  # all elements from mid to r are good
                        l = mid + 1
                    else:
                        r = mid - 1

    return count
```

## 3. Solution Explanation:

- We first sort the array in ascending order. Sorting the array allows us to use binary search to find the elements that satisfy the given conditions.
- We iterate over all pairs of elements in the array. For each pair, we perform a binary search to find the elements that satisfy the given conditions. If we find such an element, we increment the count by the number of elements in the array that are greater than or equal to the element we found.
- The time complexity of this approach is O(`n^2logn`), where `n` is the length of the array.

## 4. Complexity Analysis:
- Time complexity: O(`n^2logn`) - We iterate over all pairs of elements in the array, which takes O(`n^2`) time. For each pair, we perform a binary search to find the elements that satisfy the given conditions, which takes O(`logn`) time.
- Space complexity: O(1) - We use constant space to store the count of the good triplets.

## Topics
Array, Enumeration

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-29
