# Cheapest Flights Within K Stops

## Problem Link
[LeetCode - Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

## Difficulty
Medium

## Problem Description
<p>There are <code>n</code> cities connected by some number of flights. You are given an array <code>flights</code> where <code>flights[i] = [from<sub>i</sub>, to<sub>i</sub>, price<sub>i</sub>]</code> indicates that there is a flight from city <code>from<sub>i</sub></code> to city <code>to<sub>i</sub></code> with cost <code>price<sub>i</sub></code>.</p>

<p>You are also given three integers <code>src</code>, <code>dst</code>, and <code>k</code>, return <em><strong>the cheapest price</strong> from </em><code>src</code><em> to </em><code>dst</code><em> with at most </em><code>k</code><em> stops. </em>If there is no such route, return<em> </em><code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-3drawio.png" style="width: 332px; height: 392px;" />
<pre>
<strong>Input:</strong> n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1
<strong>Output:</strong> 700
<strong>Explanation:</strong>
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 3 is marked in red and has cost 100 + 600 = 700.
Note that the path through cities [0,1,2,3] is cheaper but is invalid because it uses 2 stops.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-1drawio.png" style="width: 332px; height: 242px;" />
<pre>
<strong>Input:</strong> n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1
<strong>Output:</strong> 200
<strong>Explanation:</strong>
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 2 is marked in red and has cost 100 + 100 = 200.
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-2drawio.png" style="width: 332px; height: 242px;" />
<pre>
<strong>Input:</strong> n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 0
<strong>Output:</strong> 500
<strong>Explanation:</strong>
The graph is shown above.
The optimal path with no stops from city 0 to 2 is marked in red and has cost 500.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 100</code></li>
	<li><code>0 &lt;= flights.length &lt;= (n * (n - 1) / 2)</code></li>
	<li><code>flights[i].length == 3</code></li>
	<li><code>0 &lt;= from<sub>i</sub>, to<sub>i</sub> &lt; n</code></li>
	<li><code>from<sub>i</sub> != to<sub>i</sub></code></li>
	<li><code>1 &lt;= price<sub>i</sub> &lt;= 10<sup>4</sup></code></li>
	<li>There will not be any multiple flights between two cities.</li>
	<li><code>0 &lt;= src, dst, k &lt; n</code></li>
	<li><code>src != dst</code></li>
</ul>


## Test Cases
```
4
[[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]]
0
3
1
3
[[0,1,100],[1,2,100],[0,2,500]]
0
2
1
3
[[0,1,100],[1,2,100],[0,2,500]]
0
2
0
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:

- This problem is a variant of the classic Dijkstra's algorithm for finding the shortest path in a graph, but with the additional constraint of limiting the number of stops.

- A straightforward approach is to use a BFS (breadth-first search) to explore all possible paths from the source to the destination within the given number of stops, keeping track of the minimum cost path.

- A more efficient approach is to use dynamic programming, where we keep track of the minimum cost to reach each city with a given number of stops.

2. Solution Implementation:
```python
import sys

def find_cheapest_price(n: int, flights: list[list[int]], src: int, dst: int, k: int) -> int:
    """
    Finds the cheapest price from src to dst with at most k stops.

    Args:
    n: The number of cities.
    flights: A list of tuples representing the flights, where each tuple is (from, to, price).
    src: The source city.
    dst: The destination city.
    k: The maximum number of stops allowed.

    Returns:
    The cheapest price from src to dst with at most k stops, or -1 if there is no such route.
    """

    # Create a graph to represent the flights.
    graph = [[] for _ in range(n)]
    for flight in flights:
        graph[flight[0]].append((flight[1], flight[2]))

    # Initialize the distance to each city with a given number of stops to infinity.
    dp = [[sys.maxsize] * (k + 1) for _ in range(n)]
    dp[src][0] = 0

    # Iterate over the number of stops.
    for i in range(1, k + 1):
        # Iterate over each city.
        for city in range(n):
            # Iterate over each flight from the current city.
            for neighbor, cost in graph[city]:
                # Update the distance to the neighbor if it is less than the current distance.
                dp[neighbor][i] = min(dp[neighbor][i], dp[city][i - 1] + cost)

    # Return the minimum distance to the destination city.
    return dp[dst][k] if dp[dst][k] != sys.maxsize else -1
```

3. Solution Explanation:

- The solution uses dynamic programming to keep track of the minimum cost to reach each city with a given number of stops.

- We initialize the distance to each city with a given number of stops to infinity, and set the distance to the source city with 0 stops to 0.

- We then iterate over the number of stops, and for each stop, we iterate over each city and update the distance to each neighbor if it is less than the current distance.

- After iterating over all the stops, we return the minimum distance to the destination city.

4. Complexity Analysis:

- Time complexity: O(n * k * m), where n is the number of cities, k is the maximum number of stops, and m is the number of flights.

- Space complexity: O(n * k), since we store the minimum cost to reach each city with a given number of stops in a 2D array.

## Topics
Dynamic Programming, Depth-First Search, Breadth-First Search, Graph, Heap (Priority Queue), Shortest Path

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-05
