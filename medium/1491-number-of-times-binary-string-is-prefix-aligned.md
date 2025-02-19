# Number of Times Binary String Is Prefix-Aligned

## Problem Link
[LeetCode - Number of Times Binary String Is Prefix-Aligned](https://leetcode.com/problems/number-of-times-binary-string-is-prefix-aligned/)

## Difficulty
Medium

## Problem Description
<p>You have a <strong>1-indexed</strong> binary string of length <code>n</code> where all the bits are <code>0</code> initially. We will flip all the bits of this binary string (i.e., change them from <code>0</code> to <code>1</code>) one by one. You are given a <strong>1-indexed</strong> integer array <code>flips</code> where <code>flips[i]</code> indicates that the bit at index <code>i</code> will be flipped in the <code>i<sup>th</sup></code> step.</p>

<p>A binary string is <strong>prefix-aligned</strong> if, after the <code>i<sup>th</sup></code> step, all the bits in the <strong>inclusive</strong> range <code>[1, i]</code> are ones and all the other bits are zeros.</p>

<p>Return <em>the number of times the binary string is <strong>prefix-aligned</strong> during the flipping process</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> flips = [3,2,4,1,5]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The binary string is initially &quot;00000&quot;.
After applying step 1: The string becomes &quot;00100&quot;, which is not prefix-aligned.
After applying step 2: The string becomes &quot;01100&quot;, which is not prefix-aligned.
After applying step 3: The string becomes &quot;01110&quot;, which is not prefix-aligned.
After applying step 4: The string becomes &quot;11110&quot;, which is prefix-aligned.
After applying step 5: The string becomes &quot;11111&quot;, which is prefix-aligned.
We can see that the string was prefix-aligned 2 times, so we return 2.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> flips = [4,1,2,3]
<strong>Output:</strong> 1
<strong>Explanation:</strong> The binary string is initially &quot;0000&quot;.
After applying step 1: The string becomes &quot;0001&quot;, which is not prefix-aligned.
After applying step 2: The string becomes &quot;1001&quot;, which is not prefix-aligned.
After applying step 3: The string becomes &quot;1101&quot;, which is not prefix-aligned.
After applying step 4: The string becomes &quot;1111&quot;, which is prefix-aligned.
We can see that the string was prefix-aligned 1 time, so we return 1.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == flips.length</code></li>
	<li><code>1 &lt;= n &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>flips</code> is a permutation of the integers in the range <code>[1, n]</code>.</li>
</ul>


## Test Cases
```
[3,2,4,1,5]
[4,1,2,3]
```

## Initial Template
```python
# Code template not available
```

## Solution
### 1. Initial Thoughts:
- The problem is about finding the number of times a binary string is prefix-aligned during the flipping process.
- The binary string is initially all 0s, and we flip the bits one by one according to the given `flips` array.
- A binary string is prefix-aligned if all the bits in the inclusive range [1, i] are ones and all the other bits are zeros after the ith step.
- We can iterate through the flips array and check if the binary string is prefix-aligned after each flip. If it is, we increment the count.

### 2. Solution Implementation:
```python
def count_binary_aligned(flips):
    """
    :type flips: List[int]
    :rtype: int
    """
    # Initialize the binary string to all 0s.
    binary_string = "0" * len(flips)
    # Initialize the count of prefix-aligned strings to 0.
    count = 0

    # Iterate through the flips array.
    for flip in flips:
        # Flip the bit at the given index.
        binary_string = binary_string[:flip-1] + "1" + binary_string[flip:]

        # Check if the binary string is prefix-aligned.
        if binary_string.startswith("1") and binary_string.endswith("0"):
            count += 1

    # Return the count of prefix-aligned strings.
    return count
```

### 3. Solution Explanation:
- The solution starts by initializing the binary string to all 0s and the count of prefix-aligned strings to 0.
- Then, it iterates through the flips array and flips the bit at the given index.
- After each flip, it checks if the binary string is prefix-aligned. If it is, it increments the count.
- Finally, the solution returns the count of prefix-aligned strings.

### 4. Complexity Analysis:
- Time complexity: O(n), where n is the length of the flips array. The solution iterates through the flips array once, and each flip takes constant time.
- Space complexity: O(n), where n is the length of the flips array. The solution stores the binary string, which is a string of length n.

## Topics
Array

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-19
