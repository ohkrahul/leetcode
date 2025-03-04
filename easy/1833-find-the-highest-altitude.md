# Find the Highest Altitude

## Problem Link
[LeetCode - Find the Highest Altitude](https://leetcode.com/problems/find-the-highest-altitude/)

## Difficulty
Easy

## Problem Description
<p>There is a biker going on a road trip. The road trip consists of <code>n + 1</code> points at different altitudes. The biker starts his trip on point <code>0</code> with altitude equal <code>0</code>.</p>

<p>You are given an integer array <code>gain</code> of length <code>n</code> where <code>gain[i]</code> is the <strong>net gain in altitude</strong> between points <code>i</code>​​​​​​ and <code>i + 1</code> for all (<code>0 &lt;= i &lt; n)</code>. Return <em>the <strong>highest altitude</strong> of a point.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> gain = [-5,1,5,0,-7]
<strong>Output:</strong> 1
<strong>Explanation:</strong> The altitudes are [0,-5,-4,1,1,-6]. The highest is 1.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> gain = [-4,-3,-2,-1,4,3,2]
<strong>Output:</strong> 0
<strong>Explanation:</strong> The altitudes are [0,-4,-7,-9,-10,-6,-3,-1]. The highest is 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == gain.length</code></li>
	<li><code>1 &lt;= n &lt;= 100</code></li>
	<li><code>-100 &lt;= gain[i] &lt;= 100</code></li>
</ul>


## Test Cases
```
[-5,1,5,0,-7]
[-4,-3,-2,-1,4,3,2]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks for the highest altitude reached during the biker's trip.
   - We're given the gain in altitude between consecutive points.
   - The biker starts at altitude 0.
   - We need to calculate the altitude at each point and keep track of the highest one.
   - A simple iterative approach should suffice. We can maintain a running sum of the gains and update the maximum altitude seen so far.

2. Solution Implementation:
```python
def largestAltitude(gain):
    """
    Finds the highest altitude reached during a bike trip.

    Args:
        gain: A list of integers representing the net gain in altitude between consecutive points.

    Returns:
        The highest altitude reached during the trip.
    """
    current_altitude = 0
    max_altitude = 0

    for g in gain:
        current_altitude += g  # Update current altitude based on gain
        max_altitude = max(max_altitude, current_altitude) # Check if current is the new max

    return max_altitude # Return the overall max altitude reached.
```

3. Solution Explanation:
   - The `largestAltitude` function takes the `gain` array as input.
   - It initializes `current_altitude` and `max_altitude` to 0.
   - It iterates through the `gain` array.
   - In each iteration, it updates `current_altitude` by adding the current gain `g`.
   - It then updates `max_altitude` if `current_altitude` is greater than the current `max_altitude`.
   - Finally, it returns `max_altitude`.

4. Complexity Analysis:
   - Time complexity: O(n) - We iterate through the `gain` array once.
   - Space complexity: O(1) - We only use a few constant extra variables. No scaling data structures used.


## Topics
Array, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-04
