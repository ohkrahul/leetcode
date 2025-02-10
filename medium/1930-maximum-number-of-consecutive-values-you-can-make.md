# Maximum Number of Consecutive Values You Can Make

## Problem Link
[LeetCode - Maximum Number of Consecutive Values You Can Make](https://leetcode.com/problems/maximum-number-of-consecutive-values-you-can-make/)

## Difficulty
Medium

## Problem Description
<p>You are given an integer array <code>coins</code> of length <code>n</code> which represents the <code>n</code> coins that you own. The value of the <code>i<sup>th</sup></code> coin is <code>coins[i]</code>. You can <strong>make</strong> some value <code>x</code> if you can choose some of your <code>n</code> coins such that their values sum up to <code>x</code>.</p>

<p>Return the <em>maximum number of consecutive integer values that you <strong>can</strong> <strong>make</strong> with your coins <strong>starting</strong> from and <strong>including</strong> </em><code>0</code>.</p>

<p>Note that you may have multiple coins of the same value.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> coins = [1,3]
<strong>Output:</strong> 2
<strong>Explanation: </strong>You can make the following values:
- 0: take []
- 1: take [1]
You can make 2 consecutive integer values starting from 0.</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> coins = [1,1,1,4]
<strong>Output:</strong> 8
<strong>Explanation: </strong>You can make the following values:
- 0: take []
- 1: take [1]
- 2: take [1,1]
- 3: take [1,1,1]
- 4: take [4]
- 5: take [4,1]
- 6: take [4,1,1]
- 7: take [4,1,1,1]
You can make 8 consecutive integer values starting from 0.</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> coins = [1,4,10,3,1]
<strong>Output:</strong> 20</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>coins.length == n</code></li>
	<li><code>1 &lt;= n &lt;= 4 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= coins[i] &lt;= 4 * 10<sup>4</sup></code></li>
</ul>


## Test Cases
```
[1,3]
[1,1,1,4]
[1,4,10,3,1]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - **Problem analysis:** We need to determine the maximum number of consecutive integer values that we can make using a given array of coins.
   - **Key observations:**
     - The coins can be used multiple times.
     - The values that we can make must be consecutive integers.
   - **Possible approaches:**
     - **Brute force:** Try all possible combinations of coins to calculate the maximum number of consecutive integers we can make.
     - **Greedy:** Sort the coins and start with the smallest coin. Keep adding coins until we can't make the next consecutive integer value.

2. **Solution Implementation:**
```python
def getMaximumConsecutive(coins):
    """
    :type coins: List[int]
    :rtype: int
    """
    # Sort the coins in ascending order
    coins.sort()

    # Initialize the maximum consecutive value to 1
    max_consecutive = 1

    # Initialize the current consecutive value to 0
    current_consecutive = 0

    # Iterate over the sorted coins
    for coin in coins:
        # If the current coin is equal to the previous coin + 1, increment the current consecutive value
        if coin == coins[current_consecutive] + 1:
            current_consecutive += 1
        # Otherwise, reset the current consecutive value to 1
        else:
            current_consecutive = 1

        # Update the maximum consecutive value if necessary
        max_consecutive = max(max_consecutive, current_consecutive)

    # Return the maximum consecutive value
    return max_consecutive
```

3. **Solution Explanation:**

   - We sort the coins in ascending order to make it easier to determine which coins can be used to make consecutive values.
   - We initialize the maximum consecutive value to 1 and the current consecutive value to 0.
   - We iterate over the sorted coins and update the current consecutive value based on whether the current coin can be used to make the next consecutive value.
   - If the current coin can be used to make the next consecutive value, we increment the current consecutive value. Otherwise, we reset the current consecutive value to 1.
   - We update the maximum consecutive value if necessary, and return the maximum consecutive value.

4. **Complexity Analysis:**

   - **Time complexity:** O(n log n), where n is the number of coins. Sorting the coins takes O(n log n) time, and iterating over the sorted coins takes O(n) time.
   - **Space complexity:** O(1), since we don't allocate any additional space for data structures.

## Topics
Array, Greedy, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-10
