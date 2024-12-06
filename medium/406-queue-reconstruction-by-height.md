# Queue Reconstruction by Height

## Problem Link
[LeetCode - Queue Reconstruction by Height](https://leetcode.com/problems/queue-reconstruction-by-height/)

## Difficulty
Medium

## Problem Description
<p>You are given an array of people, <code>people</code>, which are the attributes of some people in a queue (not necessarily in order). Each <code>people[i] = [h<sub>i</sub>, k<sub>i</sub>]</code> represents the <code>i<sup>th</sup></code> person of height <code>h<sub>i</sub></code> with <strong>exactly</strong> <code>k<sub>i</sub></code> other people in front who have a height greater than or equal to <code>h<sub>i</sub></code>.</p>

<p>Reconstruct and return <em>the queue that is represented by the input array </em><code>people</code>. The returned queue should be formatted as an array <code>queue</code>, where <code>queue[j] = [h<sub>j</sub>, k<sub>j</sub>]</code> is the attributes of the <code>j<sup>th</sup></code> person in the queue (<code>queue[0]</code> is the person at the front of the queue).</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> people = [[7,0],[4,4],[7,1],[5,0],[6,1],[5,2]]
<strong>Output:</strong> [[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]]
<strong>Explanation:</strong>
Person 0 has height 5 with no other people taller or the same height in front.
Person 1 has height 7 with no other people taller or the same height in front.
Person 2 has height 5 with two persons taller or the same height in front, which is person 0 and 1.
Person 3 has height 6 with one person taller or the same height in front, which is person 1.
Person 4 has height 4 with four people taller or the same height in front, which are people 0, 1, 2, and 3.
Person 5 has height 7 with one person taller or the same height in front, which is person 1.
Hence [[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]] is the reconstructed queue.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> people = [[6,0],[5,0],[4,0],[3,2],[2,2],[1,4]]
<strong>Output:</strong> [[4,0],[5,0],[2,2],[3,2],[1,4],[6,0]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= people.length &lt;= 2000</code></li>
	<li><code>0 &lt;= h<sub>i</sub> &lt;= 10<sup>6</sup></code></li>
	<li><code>0 &lt;= k<sub>i</sub> &lt; people.length</code></li>
	<li>It is guaranteed that the queue can be reconstructed.</li>
</ul>


## Test Cases
```
[[7,0],[4,4],[7,1],[5,0],[6,1],[5,2]]
[[6,0],[5,0],[4,0],[3,2],[2,2],[1,4]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - The problem is to reconstruct a queue from the attributes of the people in the queue.
   - Each person has a height and a count of the number of people in front of them who are taller or the same height.
   - We can use the count to determine the order of the people in the queue.

2. **Solution Implementation:**
```python
import bisect

def reconstructQueue(people):
    """
    Reconstructs a queue from the attributes of the people in the queue.

    Parameters:
    people:  A list of tuples [(h1, k1), (h2, k2), ..., (hn, kn)] where hi is the height of the ith person and ki is the number of people in front of the ith person who have a height greater than or equal to hi.

    Returns:
    A list of tuples [(h1, k1), (h2, k2), ..., (hn, kn)] representing the reconstructed queue.
    """
    # Sort the people in ascending order of height
    people.sort(key=lambda x: x[0])

    # Create a list to store the reconstructed queue
    queue = []

    # Iterate over the people
    for person in people:
        # Insert the person into the queue at the correct position
        bisect.insort(queue, person, key=lambda x: x[1])

    # Return the reconstructed queue
    return queue
```

3. **Solution Explanation:**

   - We first sort the people in ascending order of height. This makes it easier to determine the order of the people in the queue.
   - We then create a list to store the reconstructed queue.
   - We iterate over the people and insert each person into the queue at the correct position. The correct position is determined by the person's count.
   - We finally return the reconstructed queue.

4. **Complexity Analysis:**

   - Time complexity: O(n log n). Sorting the people takes O(n log n) time and inserting each person into the queue takes O(n) time.
   - Space complexity: O(n). We store the reconstructed queue in a list, which takes O(n) space.

## Topics
Array, Binary Indexed Tree, Segment Tree, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-06
