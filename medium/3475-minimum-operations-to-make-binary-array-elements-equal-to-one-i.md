# Minimum Operations to Make Binary Array Elements Equal to One I

## Problem Link
[LeetCode - Minimum Operations to Make Binary Array Elements Equal to One I](https://leetcode.com/problems/minimum-operations-to-make-binary-array-elements-equal-to-one-i/)

## Difficulty
Medium

## Problem Description
<p>You are given a <span data-keyword="binary-array">binary array</span> <code>nums</code>.</p>

<p>You can do the following operation on the array <strong>any</strong> number of times (possibly zero):</p>

<ul>
	<li>Choose <strong>any</strong> 3 <strong>consecutive</strong> elements from the array and <strong>flip</strong> <strong>all</strong> of them.</li>
</ul>

<p><strong>Flipping</strong> an element means changing its value from 0 to 1, and from 1 to 0.</p>

<p>Return the <strong>minimum</strong> number of operations required to make all elements in <code>nums</code> equal to 1. If it is impossible, return -1.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [0,1,1,1,0,0]</span></p>

<p><strong>Output:</strong> <span class="example-io">3</span></p>

<p><strong>Explanation:</strong><br />
We can do the following operations:</p>

<ul>
	<li>Choose the elements at indices 0, 1 and 2. The resulting array is <code>nums = [<u><strong>1</strong></u>,<u><strong>0</strong></u>,<u><strong>0</strong></u>,1,0,0]</code>.</li>
	<li>Choose the elements at indices 1, 2 and 3. The resulting array is <code>nums = [1,<u><strong>1</strong></u>,<u><strong>1</strong></u>,<strong><u>0</u></strong>,0,0]</code>.</li>
	<li>Choose the elements at indices 3, 4 and 5. The resulting array is <code>nums = [1,1,1,<strong><u>1</u></strong>,<u><strong>1</strong></u>,<u><strong>1</strong></u>]</code>.</li>
</ul>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [0,1,1,1]</span></p>

<p><strong>Output:</strong> <span class="example-io">-1</span></p>

<p><strong>Explanation:</strong><br />
It is impossible to make all elements equal to 1.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 1</code></li>
</ul>


## Test Cases
```
[0,1,1,1,0,0]
[0,1,1,1]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks for the minimum number of operations to make all elements in a binary array equal to 1.  We can only flip 3 consecutive elements at a time.
   - Key Observation:  If we flip at index `i`, the elements at `i`, `i+1`, and `i+2` are flipped. This means that the only way to affect the value at index `i` is by flipping at `i-2`, `i-1` or `i`.
   - Possible Approach: We can try a greedy approach. If we encounter a 0, we flip starting from that index. Then we continue. If we find a solution where all are 1s, we return the count. If we encounter an impossible situation (like trying to flip beyond array bounds), we return -1. Since the constraints are not huge, we could also explore a backtracking solution with memoization for possible optimization, though greedy feels more intuitive.

2. Solution Implementation:
```python
def minOperations(nums):
    n = len(nums)
    count = 0
    nums = nums[:]  # Create a copy to avoid modifying the original

    for i in range(n - 2):  # Iterate up to n-3 because we flip 3 elements at a time
        if nums[i] == 0:
            count += 1
            nums[i] ^= 1  # Flip current element
            nums[i + 1] ^= 1  # Flip next element
            nums[i + 2] ^= 1  # Flip the element after that

    # Check if the last two elements are 1s. If not, it's impossible
    if nums[n - 2] == 0 or nums[n - 1] == 0:
        return -1
    return count

```

3. Solution Explanation:
   - The solution iterates through the array until the `n-3` index. Whenever we encounter a 0, we flip the current element and the next two. We increment our operation count.
   - After the main loop, we check if the last two elements are 1s. If any of them are 0, it means it's impossible to make them 1 using the given operation, so we return -1.
   - This greedy approach works because flipping at index `i` only affects elements from `i` to `i+2`. Therefore, if we encounter a 0 at index `i`, we must flip starting at `i` to make it a 1. Subsequent flips might change it back to 0, but those flips are necessary to address 0s that come later.

4. Complexity Analysis:
   - Time complexity: O(N) - We iterate through the array once.
   - Space complexity: O(1) if we modify the input array in-place. As written, it uses O(N) to create a copy of `nums`, but that's easily avoided by operating directly on the input array.


## Topics
Array, Bit Manipulation, Queue, Sliding Window, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-05-02
