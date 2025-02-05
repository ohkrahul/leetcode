# Button with Longest Push Time

## Problem Link
[LeetCode - Button with Longest Push Time](https://leetcode.com/problems/button-with-longest-push-time/)

## Difficulty
Easy

## Problem Description
<p>You are given a 2D array <code>events</code> which represents a sequence of events where a child pushes a series of buttons on a keyboard.</p>

<p>Each <code>events[i] = [index<sub>i</sub>, time<sub>i</sub>]</code> indicates that the button at index <code>index<sub>i</sub></code> was pressed at time <code>time<sub>i</sub></code>.</p>

<ul>
	<li>The array is <strong>sorted</strong> in increasing order of <code>time</code>.</li>
	<li>The time taken to press a button is the difference in time between consecutive button presses. The time for the first button is simply the time at which it was pressed.</li>
</ul>

<p>Return the <code>index</code> of the button that took the <strong>longest</strong> time to push. If multiple buttons have the same longest time, return the button with the <strong>smallest</strong> <code>index</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">events = [[1,2],[2,5],[3,9],[1,15]]</span></p>

<p><strong>Output:</strong> <span class="example-io">1</span></p>

<p><strong>Explanation:</strong></p>

<ul>
	<li>Button with index 1 is pressed at time 2.</li>
	<li>Button with index 2 is pressed at time 5, so it took <code>5 - 2 = 3</code> units of time.</li>
	<li>Button with index 3 is pressed at time 9, so it took <code>9 - 5 = 4</code> units of time.</li>
	<li>Button with index 1 is pressed again at time 15, so it took <code>15 - 9 = 6</code> units of time.</li>
</ul>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">events = [[10,5],[1,7]]</span></p>

<p><strong>Output:</strong> <span class="example-io">10</span></p>

<p><strong>Explanation:</strong></p>

<ul>
	<li>Button with index 10 is pressed at time 5.</li>
	<li>Button with index 1 is pressed at time 7, so it took <code>7 - 5 = 2</code> units of time.</li>
</ul>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= events.length &lt;= 1000</code></li>
	<li><code>events[i] == [index<sub>i</sub>, time<sub>i</sub>]</code></li>
	<li><code>1 &lt;= index<sub>i</sub>, time<sub>i</sub> &lt;= 10<sup>5</sup></code></li>
	<li>The input is generated such that <code>events</code> is sorted in increasing order of <code>time<sub>i</sub></code>.</li>
</ul>


## Test Cases
```
[[1,2],[2,5],[3,9],[1,15]]
[[10,5],[1,7]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

- **Problem analysis:** The problem requires us to find the button with the longest push time. We can assume that the push time for a button is the difference between the time it is pressed and the time the previous button was pressed (for the first button, the push time is simply the time it was pressed).

- **Key observations:** The problem statement mentions that the events are sorted in increasing order of time. This means we can iterate through the events sequentially and keep track of the longest push time and the corresponding button index.

- **Possible approaches:**
    - Brute force: Iterate through all the events and compute the push time for each button. Keep track of the maximum push time and the corresponding button index.
    - Linear scan: Iterate through the events sequentially and keep track of the longest push time and the corresponding button index. The push time for a button is simply the difference between the current time and the time the previous button was pressed.

2. **Solution Implementation:**

```python
def longestPush(events):
    # Initialize the longest push time and the corresponding button index
    max_push_time = 0
    max_push_index = 0

    # Iterate through the events
    for i in range(1, len(events)):
        # Compute the push time for the current button
        push_time = events[i][1] - events[i-1][1]

        # Update the longest push time and the corresponding button index if necessary
        if push_time > max_push_time:
            max_push_time = push_time
            max_push_index = events[i][0]

    # Return the button index with the longest push time
    return max_push_index
```

3. **Solution Explanation:**

- The provided Python solution uses the linear scan approach. It iterates through the events sequentially and keeps track of the longest push time and the corresponding button index.
- For each event, the push time is computed as the difference between the current time and the time the previous button was pressed.
- If the current push time is greater than the longest push time seen so far, the longest push time and the corresponding button index are updated.
- Finally, the function returns the button index with the longest push time.

4. **Complexity Analysis:**

- **Time complexity:** O(n), where n is the number of events. The solution iterates through the events once to compute the push time for each button.
- **Space complexity:** O(1), as the solution only requires constant space to store the longest push time and the corresponding button index.

## Topics
Array

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-05
