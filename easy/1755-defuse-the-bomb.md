# Defuse the Bomb

## Problem Link
[LeetCode - Defuse the Bomb](https://leetcode.com/problems/defuse-the-bomb/)

## Difficulty
Easy

## Problem Description
<p>You have a bomb to defuse, and your time is running out! Your informer will provide you with a <strong>circular</strong> array <code>code</code>&nbsp;of length of <code>n</code>&nbsp;and a key <code>k</code>.</p>

<p>To decrypt the code, you must replace every number. All the numbers are replaced <strong>simultaneously</strong>.</p>

<ul>
	<li>If <code>k &gt; 0</code>, replace the <code>i<sup>th</sup></code> number with the sum of the <strong>next</strong> <code>k</code> numbers.</li>
	<li>If <code>k &lt; 0</code>, replace the <code>i<sup>th</sup></code> number with the sum of the <strong>previous</strong> <code>k</code> numbers.</li>
	<li>If <code>k == 0</code>, replace the <code>i<sup>th</sup></code> number with <code>0</code>.</li>
</ul>

<p>As <code>code</code> is circular, the next element of <code>code[n-1]</code> is <code>code[0]</code>, and the previous element of <code>code[0]</code> is <code>code[n-1]</code>.</p>

<p>Given the <strong>circular</strong> array <code>code</code> and an integer key <code>k</code>, return <em>the decrypted code to defuse the bomb</em>!</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> code = [5,7,1,4], k = 3
<strong>Output:</strong> [12,10,16,13]
<strong>Explanation:</strong> Each number is replaced by the sum of the next 3 numbers. The decrypted code is [7+1+4, 1+4+5, 4+5+7, 5+7+1]. Notice that the numbers wrap around.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> code = [1,2,3,4], k = 0
<strong>Output:</strong> [0,0,0,0]
<strong>Explanation:</strong> When k is zero, the numbers are replaced by 0. 
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> code = [2,4,9,3], k = -2
<strong>Output:</strong> [12,5,6,13]
<strong>Explanation:</strong> The decrypted code is [3+9, 2+3, 4+2, 9+4]. Notice that the numbers wrap around again. If k is negative, the sum is of the <strong>previous</strong> numbers.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == code.length</code></li>
	<li><code>1 &lt;= n&nbsp;&lt;= 100</code></li>
	<li><code>1 &lt;= code[i] &lt;= 100</code></li>
	<li><code>-(n - 1) &lt;= k &lt;= n - 1</code></li>
</ul>


## Test Cases
```
[5,7,1,4]
3
[1,2,3,4]
0
[2,4,9,3]
-2
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to calculate a sum of elements in a circular array based on a key `k`.  If `k` is positive, we sum the next `k` elements. If negative, we sum the previous `k` elements. If 0, the result is 0.
   - Circular array means we need to handle wrap-around.  Modulo operator (`%`) will be useful here.
   - We can pre-calculate the sum of all elements in the array to potentially optimize the summing process, especially if `k` is large.  However, since the array size is limited to 100, a straightforward approach might be sufficient.
   - We need to create a new array to store the results as all replacements happen simultaneously.

2. Solution Implementation:
```python
def decrypt(code, k):
    n = len(code)
    result = [0] * n

    if k == 0:
        return result

    for i in range(n):
        current_sum = 0
        if k > 0:
            for j in range(1, k + 1):  # Iterate through next k elements
                current_sum += code[(i + j) % n]  # Modulo handles wrap-around
        else:  # k < 0
            for j in range(1, abs(k) + 1):  # Iterate through previous |k| elements
                current_sum += code[(i - j) % n] # Modulo handles wrap-around (negative modulo in Python works as expected)

        result[i] = current_sum

    return result
```

3. Solution Explanation:
   - We initialize a result array with zeros.
   - If `k` is 0, we return the zero-filled array immediately.
   - We iterate through each element of the `code` array (index `i`).
   - Inside the loop, we calculate the `current_sum` based on the value of `k`.
   - If `k` is positive, we iterate from `i + 1` to `i + k`, wrapping around using the modulo operator (`% n`). This ensures that if we go past the end of the array, we start back at the beginning.
   - If `k` is negative, we do a similar iteration but backwards, using `i - j`. Again, the modulo operator handles wrap-around.  Python's negative modulo works as expected here, giving the correct index within the array.
   - Finally, we store the `current_sum` in the `result` array at the corresponding index `i`.

4. Complexity Analysis:
   - Time complexity: O(n*|k|) - We have an outer loop that iterates `n` times (the length of the array) and an inner loop that iterates |k| times.
   - Space complexity: O(n) -  We use a result array of size `n` to store the decrypted code.  The space used for other variables is constant and doesn't depend on the input size.


## Topics
Array, Sliding Window

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-29
