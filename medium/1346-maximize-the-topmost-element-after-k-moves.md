# Maximize the Topmost Element After K Moves

## Problem Link
[LeetCode - Maximize the Topmost Element After K Moves](https://leetcode.com/problems/maximize-the-topmost-element-after-k-moves/)

## Difficulty
Medium

## Problem Description
<p>You are given a <strong>0-indexed</strong> integer array <code>nums</code> representing the contents of a <b>pile</b>, where <code>nums[0]</code> is the topmost element of the pile.</p>

<p>In one move, you can perform <strong>either</strong> of the following:</p>

<ul>
	<li>If the pile is not empty, <strong>remove</strong> the topmost element of the pile.</li>
	<li>If there are one or more removed elements, <strong>add</strong> any one of them back onto the pile. This element becomes the new topmost element.</li>
</ul>

<p>You are also given an integer <code>k</code>, which denotes the total number of moves to be made.</p>

<p>Return <em>the <strong>maximum value</strong> of the topmost element of the pile possible after <strong>exactly</strong></em> <code>k</code> <em>moves</em>. In case it is not possible to obtain a non-empty pile after <code>k</code> moves, return <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [5,2,2,4,0,6], k = 4
<strong>Output:</strong> 5
<strong>Explanation:</strong>
One of the ways we can end with 5 at the top of the pile after 4 moves is as follows:
- Step 1: Remove the topmost element = 5. The pile becomes [2,2,4,0,6].
- Step 2: Remove the topmost element = 2. The pile becomes [2,4,0,6].
- Step 3: Remove the topmost element = 2. The pile becomes [4,0,6].
- Step 4: Add 5 back onto the pile. The pile becomes [5,4,0,6].
Note that this is not the only way to end with 5 at the top of the pile. It can be shown that 5 is the largest answer possible after 4 moves.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [2], k = 1
<strong>Output:</strong> -1
<strong>Explanation:</strong> 
In the first move, our only option is to pop the topmost element of the pile.
Since it is not possible to obtain a non-empty pile after one move, we return -1.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i], k &lt;= 10<sup>9</sup></code></li>
</ul>


## Test Cases
```
[5,2,2,4,0,6]
4
[2]
1
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts:
- This problem is about maximizing the topmost element of a pile after a given number of moves. The pile can have several operations: pop the topmost element or add back any removed element to the top of the pile.
- A key observation is that the only way to increase the topmost element is to pop out smaller elements and add back larger elements.
- Hence, we can sort the array and always pop smaller elements first and add back larger elements.

## Solution Implementation:
```python
class Solution:
    def maxValueAfterReverse(self, nums: List[int], k: int) -> int:
        # Sort the array in ascending order
        nums.sort()
        
        # Initialize the index of the topmost element
        top = 0
        
        # Perform k moves
        for i in range(k):
            # If the topmost element is not the largest, swap it with the largest element
            if nums[top] < nums[-1]:
                nums[top], nums[-1] = nums[-1], nums[top]
                # Update the index of the topmost element
                top += 1
        
        # Return the topmost element
        return nums[top]
```

## Solution Explanation:
- We initialize a variable `top` to the index of the topmost element of the pile.
- We then start a loop for `k` moves and in each move, we check if the topmost element is the largest element in the pile. If it isn't, we swap the topmost element with the largest element to maximize the top element.
- After `k` moves, we return the topmost element in the pile.

## Complexity Analysis:
- **Time complexity**: `O(nlogn)`
- **Space complexity**: `O(1)`

## Topics
Array, Greedy

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-13
