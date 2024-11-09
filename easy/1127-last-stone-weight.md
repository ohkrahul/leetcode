# Last Stone Weight

## Problem Link
[LeetCode - Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)

## Difficulty
Easy

## Problem Description
<p>You are given an array of integers <code>stones</code> where <code>stones[i]</code> is the weight of the <code>i<sup>th</sup></code> stone.</p>

<p>We are playing a game with the stones. On each turn, we choose the <strong>heaviest two stones</strong> and smash them together. Suppose the heaviest two stones have weights <code>x</code> and <code>y</code> with <code>x &lt;= y</code>. The result of this smash is:</p>

<ul>
	<li>If <code>x == y</code>, both stones are destroyed, and</li>
	<li>If <code>x != y</code>, the stone of weight <code>x</code> is destroyed, and the stone of weight <code>y</code> has new weight <code>y - x</code>.</li>
</ul>

<p>At the end of the game, there is <strong>at most one</strong> stone left.</p>

<p>Return <em>the weight of the last remaining stone</em>. If there are no stones left, return <code>0</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> stones = [2,7,4,1,8,1]
<strong>Output:</strong> 1
<strong>Explanation:</strong> 
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that&#39;s the value of the last stone.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> stones = [1]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= stones.length &lt;= 30</code></li>
	<li><code>1 &lt;= stones[i] &lt;= 1000</code></li>
</ul>


## Test Cases
```
[2,7,4,1,8,1]
[1]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:

- Problem analysis:
   - We are given an array of stones with their weights. 
   - We need to find the weight of the last stone remaining after a series of smashes.

- Key observations:
   - In each smash, we choose the heaviest two stones.
   - If the weights are equal, both stones are destroyed.
   - If the weights are different, the heavier stone is destroyed and the lighter stone has its weight reduced by the weight of the heavier stone.
   - The game continues until there is only one stone left or no stones left.

- Possible approaches:
   - **Greedy approach:** We can use a min-heap to keep track of the stone weights. In each smash, we remove the two heaviest stones and update the weight of the remaining stone accordingly. This approach has a time complexity of O(n log n), where n is the number of stones.
   - **Simulation approach:** We can simulate the game by repeatedly merging the two heaviest stones until there is only one stone left or no stones left. This approach has a time complexity of O(n^2).

2. Solution Implementation:

```python
import heapq

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        # Create a min-heap to store the stone weights
        stone_heap = [-stone for stone in stones]
        heapq.heapify(stone_heap)

        # While there are at least two stones in the heap
        while len(stone_heap) >= 2:
            # Remove the two heaviest stones
            stone1 = heapq.heappop(stone_heap)
            stone2 = heapq.heappop(stone_heap)

            # If the stones have equal weights, both are destroyed
            if stone1 == stone2:
                continue

            # Otherwise, update the weight of the remaining stone
            new_stone = stone1 + stone2
            heapq.heappush(stone_heap, -new_stone)

        # Return the weight of the last remaining stone, or 0 if no stones are left
        if stone_heap:
            return -stone_heap[0]
        else:
            return 0
```

3. Solution Explanation:

- We use a min-heap to keep track of the stone weights in ascending order.
- In each smash, we remove the two heaviest stones from the heap.
- If the weights are equal, both stones are destroyed and we continue to the next smash.
- If the weights are different, the heavier stone is destroyed and the lighter stone has its weight reduced by the weight of the heavier stone.
- We continue this process until there is only one stone left or no stones left.
- Finally, we return the weight of the last remaining stone, or 0 if no stones are left.

4. Complexity Analysis:

- Time complexity: O(n log n), where n is the number of stones.
- Space complexity: O(n), since we store all the stone weights in a heap.

## Topics
Array, Heap (Priority Queue)

Solved on: 2024-11-09
