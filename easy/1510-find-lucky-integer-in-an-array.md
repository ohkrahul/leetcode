# Find Lucky Integer in an Array

## Problem Link
[LeetCode - Find Lucky Integer in an Array](https://leetcode.com/problems/find-lucky-integer-in-an-array/)

## Difficulty
Easy

## Problem Description
<p>Given an array of integers <code>arr</code>, a <strong>lucky integer</strong> is an integer that has a frequency in the array equal to its value.</p>

<p>Return <em>the largest <strong>lucky integer</strong> in the array</em>. If there is no <strong>lucky integer</strong> return <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> arr = [2,2,3,4]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The only lucky number in the array is 2 because frequency[2] == 2.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> arr = [1,2,2,3,3,3]
<strong>Output:</strong> 3
<strong>Explanation:</strong> 1, 2 and 3 are all lucky numbers, return the largest of them.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> arr = [2,2,2,3,3]
<strong>Output:</strong> -1
<strong>Explanation:</strong> There are no lucky numbers in the array.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= arr.length &lt;= 500</code></li>
	<li><code>1 &lt;= arr[i] &lt;= 500</code></li>
</ul>


## Test Cases
```
[2,2,3,4]
[1,2,2,3,3,3]
[2,2,2,3,3]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to find the largest "lucky integer" in an array. A lucky integer is one whose value is equal to its frequency in the array.
   - We can use a hash map (dictionary in Python) to store the frequencies of each number in the array.
   - Then, we can iterate through the array or the dictionary keys and check if any number is a lucky integer.  We'll keep track of the largest lucky integer seen so far.
   - If no lucky integer is found, we return -1.

2. Solution Implementation:
```python
def findLucky(arr):
    """
    Finds the largest lucky integer in an array.

    Args:
        arr: The input array of integers.

    Returns:
        The largest lucky integer, or -1 if none exists.
    """
    freq = {}  # Dictionary to store frequencies
    for num in arr:
        freq[num] = freq.get(num, 0) + 1  # Count frequencies

    largest_lucky = -1  # Initialize to -1

    for num in freq:  # Iterate through the numbers seen
        if num == freq[num]:  # Check if it's a lucky integer
            largest_lucky = max(largest_lucky, num)  # Update largest

    return largest_lucky
```

3. Solution Explanation:
   - The code first creates a dictionary `freq` to store the frequencies of each number in the input array `arr`.
   - It iterates through `arr`, incrementing the count for each number in `freq`.
   - `largest_lucky` is initialized to -1.
   - The code then iterates through the keys (numbers) in the `freq` dictionary.
   - Inside the loop, it checks if the current number `num` is a lucky integer (i.e., `num == freq[num]`).
   - If it is, `largest_lucky` is updated with the maximum of its current value and `num`.
   - Finally, the function returns `largest_lucky`.


4. Complexity Analysis:
   - Time complexity: O(n) - We iterate through the array once to build the frequency map and then at most again when checking the numbers which have appeared.  Even though we have nested loops, it would be at most 2n, still O(n) when dropping constants.
   - Space complexity: O(n) - In the worst-case scenario (all numbers are distinct), the frequency map can store up to 'n' unique elements. In average cases, it will likely use less space, especially with the constraints the numbers must be within 1-500. However, worst-case is linear, so we use that as our notation. 


## Topics
Array, Hash Table, Counting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-17
