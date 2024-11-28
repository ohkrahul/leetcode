# Minimum Numbers of Function Calls to Make Target Array

## Problem Link
[LeetCode - Minimum Numbers of Function Calls to Make Target Array](https://leetcode.com/problems/minimum-numbers-of-function-calls-to-make-target-array/)

## Difficulty
Medium

## Problem Description
<p>You are given an integer array <code>nums</code>. You have an integer array <code>arr</code> of the same length with all values set to <code>0</code> initially. You also have the following <code>modify</code> function:</p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/07/10/sample_2_1887.png" style="width: 573px; height: 294px;" />
<p>You want to use the modify function to convert <code>arr</code> to <code>nums</code> using the minimum number of calls.</p>

<p>Return <em>the minimum number of function calls to make </em><code>nums</code><em> from </em><code>arr</code>.</p>

<p>The test cases are generated so that the answer fits in a <strong>32-bit</strong> signed integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,5]
<strong>Output:</strong> 5
<strong>Explanation:</strong> Increment by 1 (second element): [0, 0] to get [0, 1] (1 operation).
Double all the elements: [0, 1] -&gt; [0, 2] -&gt; [0, 4] (2 operations).
Increment by 1 (both elements)  [0, 4] -&gt; [1, 4] -&gt; <strong>[1, 5]</strong> (2 operations).
Total of operations: 1 + 2 + 2 = 5.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,2]
<strong>Output:</strong> 3
<strong>Explanation:</strong> Increment by 1 (both elements) [0, 0] -&gt; [0, 1] -&gt; [1, 1] (2 operations).
Double all the elements: [1, 1] -&gt; <strong>[2, 2]</strong> (1 operation).
Total of operations: 2 + 1 = 3.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [4,2,5]
<strong>Output:</strong> 6
<strong>Explanation:</strong> (initial)[0,0,0] -&gt; [1,0,0] -&gt; [1,0,1] -&gt; [2,0,2] -&gt; [2,1,2] -&gt; [4,2,4] -&gt; <strong>[4,2,5]</strong>(nums).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
</ul>


## Test Cases
```
[1,5]
[2,2]
[4,2,5]
```

## Initial Template
```python
# Code template not available
```

## Solution
### Initial Thoughts

- The problem requires us to convert an array to another array using the provided `modify()` function. The goal is to make this conversion using the minimum number of function calls.
- Key observations:
  - The `modify()` function can be used to increment by 1 or double the value of each element in the array.
  - The problem can be broken down into smaller subproblems:
    - Incrementing each element by 1
    - Doubling each element
    - Combining these operations to reach the target array
- Possible approaches:
  - Recursive approach: This involves breaking the problem into smaller subproblems and recursively calling the function with different target values.
  - Iterative approach: This involves iteratively performing the necessary operations until the target array is reached.

### Solution Implementation
```python
def minOperations(nums):
  """
  :type nums: List[int]
  :rtype: int
  """
  
  # Initialize the number of operations to 0
  operations = 0
  
  # Iterate over the elements in nums
  for num in nums:
    # While num is not equal to 1, perform operations
    while num != 1:
      # If num is odd, increment operations and divide num by 2
      if num % 2 == 1:
        operations += 1
        num //= 2
      # If num is even, increment operations and divide num by 2
      else:
        operations += 1
        num //= 2
  
  # Return the number of operations
  return operations
```

### Solution Explanation

The solution uses an iterative approach to solve the problem. It iterates over the elements in the input array and performs the necessary operations to convert each element to 1. The number of operations required to convert each element is determined by the following steps:

- If the element is odd, we increment the number of operations by 1 and divide the element by 2.
- If the element is even, we increment the number of operations by 1 and divide the element by 2.

The process continues until the element reaches 1, at which point no further operations are required. The number of operations for each element is then added to the total number of operations.

### Complexity Analysis

- Time complexity: O(n), where n is the number of elements in the input array. The solution iterates over each element in the array once, performing a constant number of operations for each element.
- Space complexity: O(1), as the solution requires only a constant amount of memory, regardless of the input size.

## Topics
Array, Greedy, Bit Manipulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-28
