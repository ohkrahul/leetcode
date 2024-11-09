# Largest Values From Labels

## Problem Link
[LeetCode - Largest Values From Labels](https://leetcode.com/problems/largest-values-from-labels/)

## Difficulty
Medium

## Problem Description
<p>You are given <code>n</code> item&#39;s value and label as two integer arrays <code>values</code> and <code>labels</code>. You are also given two integers <code>numWanted</code> and <code>useLimit</code>.</p>

<p>Your task is to find a subset of items with the <strong>maximum sum</strong> of their values such that:</p>

<ul>
	<li>The number of items is <strong>at most</strong> <code>numWanted</code>.</li>
	<li>The number of items with the same label is <strong>at most</strong> <code>useLimit</code>.</li>
</ul>

<p>Return the maximum sum.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">values = [5,4,3,2,1], labels = [1,1,2,2,3], numWanted = 3, useLimit = 1</span></p>

<p><strong>Output:</strong> <span class="example-io">9</span></p>

<p><strong>Explanation:</strong></p>

<p>The subset chosen is the first, third, and fifth items with the sum of values 5 + 3 + 1.</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">values = [5,4,3,2,1], labels = [1,3,3,3,2], numWanted = 3, useLimit = 2</span></p>

<p><strong>Output:</strong> <span class="example-io">12</span></p>

<p><strong>Explanation:</strong></p>

<p>The subset chosen is the first, second, and third items with the sum of values 5 + 4 + 3.</p>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">values = [9,8,8,7,6], labels = [0,0,0,1,1], numWanted = 3, useLimit = 1</span></p>

<p><strong>Output:</strong> <span class="example-io">16</span></p>

<p><strong>Explanation:</strong></p>

<p>The subset chosen is the first and fourth items with the sum of values 9 + 7.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == values.length == labels.length</code></li>
	<li><code>1 &lt;= n &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>0 &lt;= values[i], labels[i] &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= numWanted, useLimit &lt;= n</code></li>
</ul>


## Test Cases
```
[5,4,3,2,1]
[1,1,2,2,3]
3
1
[5,4,3,2,1]
[1,3,3,3,2]
3
2
[9,8,8,7,6]
[0,0,0,1,1]
3
1
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts
- This problem is similar to the knapsack problem, but with additional constraints. We need to maximize the sum of values while satisfying two constraints: the number of items should be at most `numWanted` and the number of items with the same label should be at most `useLimit`.
- One possible approach is to use a dynamic programming technique. We can define a 2D array `dp`, where `dp[i][j]` represents the maximum sum of values that can be obtained using the first `i` items, while using `j` labels.
- We can initialize `dp[0][0]` to 0 and then fill in the rest of the array using the following logic:
```
for i in range(1, n + 1):
  for j in range(useLimit + 1):
    dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - 1] + values[i - 1]) if labels[i - 1] <= j else dp[i - 1][j]
```
- The first term in the `max` function represents the case where we do not use the current item, and the second term represents the case where we use the current item.
- Finally, we can return `dp[n][numWanted]`.


## Solution Implementation:
```python
def largestValuesFromLabels(values, labels, numWanted, useLimit):
  """
  :type values: List[int]
  :type labels: List[int]
  :type numWanted: int
  :type useLimit: int
  :rtype: int
  """
  # Sort the items by their values in descending order
  items = [(v, l) for v, l in zip(values, labels)]
  items.sort(key=lambda x: -x[0])

  # Initialize a dictionary to store the number of times each label has been used
  label_counts = {}
  
  total_value = 0
  num_items = 0

  # Iterate over the items in descending order of value
  for value, label in items:
    # If we have not used this label the maximum number of times
    if label not in label_counts or label_counts[label] < useLimit:
      # Update the number of times this label has been used
      if label not in label_counts:
        label_counts[label] = 0
      label_counts[label] += 1

      # Add the value of the item to the total
      total_value += value
      num_items += 1

    # If we have used this label the maximum number of times, or if we have selected the maximum number of items, break
    if num_items >= numWanted or label_counts[label] >= useLimit:
      break

  return total_value
```


## Solution Explanation:
The solution begins by sorting the items by their values in descending order. This ensures that the most valuable items are considered first. 
Then, the solution initializes a dictionary `label_counts` to store the number of times each label has been used.

The solution then iterates over the sorted items. For each item, it checks if the label of the item has been used less than the maximum number of times. If so, the solution updates the number of times the label has been used, adds the value of the item to the total, and increments the number of items.

If the label of the item has been used the maximum number of times, or if the number of items selected is greater than or equal to the maximum number of items, the solution breaks out of the loop.

Finally, the solution returns the total value of the selected items.


## Complexity Analysis
- **Time complexity**: O(n log n), where n is the number of items. The sorting operation takes O(n log n) time, and the iteration over the sorted items takes O(n) time.
- **Space complexity**: O(n), since we store the number of times each label has been used in a dictionary.

## Topics
Array, Hash Table, Greedy, Sorting, Counting

Solved on: 2024-11-09
