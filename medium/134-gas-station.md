# Gas Station

## Problem Link
[LeetCode - Gas Station](https://leetcode.com/problems/gas-station/)

## Difficulty
Medium

## Problem Description
<p>There are <code>n</code> gas stations along a circular route, where the amount of gas at the <code>i<sup>th</sup></code> station is <code>gas[i]</code>.</p>

<p>You have a car with an unlimited gas tank and it costs <code>cost[i]</code> of gas to travel from the <code>i<sup>th</sup></code> station to its next <code>(i + 1)<sup>th</sup></code> station. You begin the journey with an empty tank at one of the gas stations.</p>

<p>Given two integer arrays <code>gas</code> and <code>cost</code>, return <em>the starting gas station&#39;s index if you can travel around the circuit once in the clockwise direction, otherwise return</em> <code>-1</code>. If there exists a solution, it is <strong>guaranteed</strong> to be <strong>unique</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> gas = [1,2,3,4,5], cost = [3,4,5,1,2]
<strong>Output:</strong> 3
<strong>Explanation:</strong>
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> gas = [2,3,4], cost = [3,4,3]
<strong>Output:</strong> -1
<strong>Explanation:</strong>
You can&#39;t start at station 0 or 1, as there is not enough gas to travel to the next station.
Let&#39;s start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 0. Your tank = 4 - 3 + 2 = 3
Travel to station 1. Your tank = 3 - 3 + 3 = 3
You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3.
Therefore, you can&#39;t travel around the circuit once no matter where you start.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == gas.length == cost.length</code></li>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= gas[i], cost[i] &lt;= 10<sup>4</sup></code></li>
</ul>


## Test Cases
```
[1,2,3,4,5]
[3,4,5,1,2]
[2,3,4]
[3,4,3]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - We can think of this problem as traversing a circular linked list.
   - We need to find a starting point where the total gas gained is greater than the total cost to travel around the circuit.
   - A straightforward approach would be to start from each station and simulate the journey until we either run out of gas or complete the circuit.

2. **Solution Implementation:**

```python
from typing import List

def canCompleteCircuit(gas: List[int], cost: List[int]) -> int:
    """
    Problem: Gas Station
    Difficulty: Medium

    Given two integer arrays gas and cost, return the starting gas station's index if you can travel around the circuit 
    once in the clockwise direction, otherwise return -1. If there exists a solution, it is guaranteed to be unique.

    Example:
        Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
        Output: 3

    Args:
        gas: Amount of gas at each station
        cost: Cost to travel from one station to the next

    Returns:
        Starting gas station's index if you can travel around the circuit once, otherwise return -1
    """
    total_gas = 0
    current_gas = 0
    starting_station = 0

    for i in range(len(gas)):
        total_gas += gas[i] - cost[i]
        current_gas += gas[i] - cost[i]

        if current_gas < 0:
            current_gas = 0
            starting_station = i + 1

    return starting_station if total_gas >= 0 else -1
```

3. **Solution Explanation:**

   - We start from station 0 and keep track of the total gas gained and the current gas in the tank.
   - If the current gas in the tank becomes negative, we need to reset it to 0 and start from the next station.
   - We also keep track of the starting station.
   - If we complete the circuit and the total gas gained is greater than or equal to 0, we return the starting station.
   - Otherwise, we return -1.

4. **Complexity Analysis:**

   - Time complexity: O(n) - We traverse the array once.
   - Space complexity: O(1) - We only use a few constant space variables.

## Topics
Array, Greedy

Solved on: 2024-11-09
