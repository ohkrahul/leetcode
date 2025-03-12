# Fruit Into Baskets

## Problem Link
[LeetCode - Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)

## Difficulty
Medium

## Problem Description
<p>You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array <code>fruits</code> where <code>fruits[i]</code> is the <strong>type</strong> of fruit the <code>i<sup>th</sup></code> tree produces.</p>

<p>You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:</p>

<ul>
	<li>You only have <strong>two</strong> baskets, and each basket can only hold a <strong>single type</strong> of fruit. There is no limit on the amount of fruit each basket can hold.</li>
	<li>Starting from any tree of your choice, you must pick <strong>exactly one fruit</strong> from <strong>every</strong> tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.</li>
	<li>Once you reach a tree with fruit that cannot fit in your baskets, you must stop.</li>
</ul>

<p>Given the integer array <code>fruits</code>, return <em>the <strong>maximum</strong> number of fruits you can pick</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> fruits = [<u>1,2,1</u>]
<strong>Output:</strong> 3
<strong>Explanation:</strong> We can pick from all 3 trees.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> fruits = [0,<u>1,2,2</u>]
<strong>Output:</strong> 3
<strong>Explanation:</strong> We can pick from trees [1,2,2].
If we had started at the first tree, we would only pick from trees [0,1].
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> fruits = [1,<u>2,3,2,2</u>]
<strong>Output:</strong> 4
<strong>Explanation:</strong> We can pick from trees [2,3,2,2].
If we had started at the first tree, we would only pick from trees [1,2].
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= fruits.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= fruits[i] &lt; fruits.length</code></li>
</ul>


## Test Cases
```
[1,2,1]
[0,1,2,2]
[1,2,3,2,2]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - This problem looks like a sliding window problem where we want to find the longest subarray containing at most two distinct fruit types.
   - We can use a dictionary to track the frequency of each fruit type within the current window.
   - We'll maintain a left and right pointer for the window and expand it while the number of distinct fruits is less than or equal to 2. 
   - When we encounter a third fruit type, we'll shrink the window from the left until we have only two fruit types again.
   - We'll keep track of the maximum window size during the process.


2. Solution Implementation:
```python
def totalFruit(fruits):
    fruit_freq = {}  # Dictionary to store fruit frequencies in the window
    max_fruits = 0   # Maximum fruits collected so far
    left = 0       # Left pointer of the window

    for right in range(len(fruits)):
        fruit_freq[fruits[right]] = fruit_freq.get(fruits[right], 0) + 1  # Update frequency of the current fruit
        
        # If we have more than 2 fruit types, shrink the window
        while len(fruit_freq) > 2:
            fruit_freq[fruits[left]] -= 1
            if fruit_freq[fruits[left]] == 0:
                del fruit_freq[fruits[left]]  # Remove fruit if its count becomes 0
            left += 1
        
        max_fruits = max(max_fruits, right - left + 1)  # Update max_fruits

    return max_fruits
```

3. Solution Explanation:
   - We use a sliding window approach with `left` and `right` pointers.
   - The `fruit_freq` dictionary stores the frequency of each fruit type within the current window.
   - We expand the window by incrementing the `right` pointer.
   - If we encounter a third distinct fruit type (i.e., `len(fruit_freq) > 2`), we shrink the window from the left by incrementing `left` and decrementing the corresponding fruit's frequency until we have only two fruit types in the window again.
   - We continuously update `max_fruits` with the maximum window size seen so far.


4. Complexity Analysis:
   - Time complexity: O(N) - We iterate through the `fruits` array once. Each fruit is added to the `fruit_freq` dictionary and potentially removed once, which are constant time operations.
   - Space complexity: O(1) - The `fruit_freq` dictionary stores at most 3 distinct fruit types (as we are limited to 2 types). Therefore, the space used is constant regardless of the input size.  It's not O(N) because the number of distinct fruit types we store at a time is limited by the problem's constraints (2 baskets). This is crucial – our space usage doesn't scale with the input array size.


## Topics
Array, Hash Table, Sliding Window

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-12
