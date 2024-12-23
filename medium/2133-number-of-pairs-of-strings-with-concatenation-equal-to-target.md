# Number of Pairs of Strings With Concatenation Equal to Target

## Problem Link
[LeetCode - Number of Pairs of Strings With Concatenation Equal to Target](https://leetcode.com/problems/number-of-pairs-of-strings-with-concatenation-equal-to-target/)

## Difficulty
Medium

## Problem Description
<p>Given an array of <strong>digit</strong> strings <code>nums</code> and a <strong>digit</strong> string <code>target</code>, return <em>the number of pairs of indices </em><code>(i, j)</code><em> (where </em><code>i != j</code><em>) such that the <strong>concatenation</strong> of </em><code>nums[i] + nums[j]</code><em> equals </em><code>target</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [&quot;777&quot;,&quot;7&quot;,&quot;77&quot;,&quot;77&quot;], target = &quot;7777&quot;
<strong>Output:</strong> 4
<strong>Explanation:</strong> Valid pairs are:
- (0, 1): &quot;777&quot; + &quot;7&quot;
- (1, 0): &quot;7&quot; + &quot;777&quot;
- (2, 3): &quot;77&quot; + &quot;77&quot;
- (3, 2): &quot;77&quot; + &quot;77&quot;
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [&quot;123&quot;,&quot;4&quot;,&quot;12&quot;,&quot;34&quot;], target = &quot;1234&quot;
<strong>Output:</strong> 2
<strong>Explanation:</strong> Valid pairs are:
- (0, 1): &quot;123&quot; + &quot;4&quot;
- (2, 3): &quot;12&quot; + &quot;34&quot;
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [&quot;1&quot;,&quot;1&quot;,&quot;1&quot;], target = &quot;11&quot;
<strong>Output:</strong> 6
<strong>Explanation:</strong> Valid pairs are:
- (0, 1): &quot;1&quot; + &quot;1&quot;
- (1, 0): &quot;1&quot; + &quot;1&quot;
- (0, 2): &quot;1&quot; + &quot;1&quot;
- (2, 0): &quot;1&quot; + &quot;1&quot;
- (1, 2): &quot;1&quot; + &quot;1&quot;
- (2, 1): &quot;1&quot; + &quot;1&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 100</code></li>
	<li><code>1 &lt;= nums[i].length &lt;= 100</code></li>
	<li><code>2 &lt;= target.length &lt;= 100</code></li>
	<li><code>nums[i]</code> and <code>target</code> consist of digits.</li>
	<li><code>nums[i]</code> and <code>target</code> do not have leading zeros.</li>
</ul>


## Test Cases
```
["777","7","77","77"]
"7777"
["123","4","12","34"]
"1234"
["1","1","1"]
"11"
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts

- **Problem analysis**: This problem asks us to find the number of pairs of strings in an array that concatenate to a given target string.
- **Key observations**: To concatenate two strings, we simply join them together.
- **Possible approaches**: One possible approach is to use nested loops to check every pair of strings in the array and see if their concatenation equals the target. However, this approach has a time complexity of O(n^2), which is not efficient for large arrays. A more efficient approach is to use a hash table to store the count of each string in the array. Then, for each string in the array, we can check if the target minus that string is also in the hash table. If it is, then we can increment the count by the count of that string.

## 2. Solution Implementation

```python
import collections

def numOfPairs(nums, target):
  """
  :type nums: List[str]
  :type target: str
  :rtype: int
  """
  # Create a hash table to store the count of each string in the array
  hash = collections.Counter(nums)

  # Initialize the count to 0
  count = 0

  # Check each string in the array
  for num in nums:
    # Calculate the complement of the target
    complement = target.replace(num, '')

    # Check if the complement is in the hash table
    if complement in hash:
      # Increment the count by the count of the complement
      count += hash[complement]

  # Return the count
  return count
```

## 3. Solution Explanation

The solution starts by creating a hash table to store the count of each string in the array. Then, it iterates through each string in the array and calculates the complement of the target by removing that string from the target. If the complement is in the hash table, it means that the concatenation of that string with the current string equals the target. In that case, the count is incremented by the count of the complement.

## 4. Complexity Analysis

- **Time complexity**: O(n), where n is the length of the array. The solution uses a hash table to store the count of each string in the array and iterates through the array once.
- **Space complexity**: O(n), as the hash table can store up to n keys.

## Topics
Array, Hash Table, String, Counting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-23
