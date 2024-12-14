# Maximize Win From Two Segments

## Problem Link
[LeetCode - Maximize Win From Two Segments](https://leetcode.com/problems/maximize-win-from-two-segments/)

## Difficulty
Medium

## Problem Description
<p>There are some prizes on the <strong>X-axis</strong>. You are given an integer array <code>prizePositions</code> that is <strong>sorted in non-decreasing order</strong>, where <code>prizePositions[i]</code> is the position of the <code>i<sup>th</sup></code> prize. There could be different prizes at the same position on the line. You are also given an integer <code>k</code>.</p>

<p>You are allowed to select two segments with integer endpoints. The length of each segment must be <code>k</code>. You will collect all prizes whose position falls within at least one of the two selected segments (including the endpoints of the segments). The two selected segments may intersect.</p>

<ul>
	<li>For example if <code>k = 2</code>, you can choose segments <code>[1, 3]</code> and <code>[2, 4]</code>, and you will win any prize <font face="monospace">i</font> that satisfies <code>1 &lt;= prizePositions[i] &lt;= 3</code> or <code>2 &lt;= prizePositions[i] &lt;= 4</code>.</li>
</ul>

<p>Return <em>the <strong>maximum</strong> number of prizes you can win if you choose the two segments optimally</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> prizePositions = [1,1,2,2,3,3,5], k = 2
<strong>Output:</strong> 7
<strong>Explanation:</strong> In this example, you can win all 7 prizes by selecting two segments [1, 3] and [3, 5].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> prizePositions = [1,2,3,4], k = 0
<strong>Output:</strong> 2
<strong>Explanation:</strong> For this example, <strong>one choice</strong> for the segments is <code>[3, 3]</code> and <code>[4, 4],</code> and you will be able to get <code>2</code> prizes. 
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= prizePositions.length &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= prizePositions[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>0 &lt;= k &lt;= 10<sup>9</sup> </code></li>
	<li><code>prizePositions</code> is sorted in non-decreasing order.</li>
</ul>

<p>&nbsp;</p>
<style type="text/css">.spoilerbutton {display:block; border:dashed; padding: 0px 0px; margin:10px 0px; font-size:150%; font-weight: bold; color:#000000; background-color:cyan; outline:0; 
}
.spoiler {overflow:hidden;}
.spoiler > div {-webkit-transition: all 0s ease;-moz-transition: margin 0s ease;-o-transition: all 0s ease;transition: margin 0s ease;}
.spoilerbutton[value="Show Message"] + .spoiler > div {margin-top:-500%;}
.spoilerbutton[value="Hide Message"] + .spoiler {padding:5px;}
</style>


## Test Cases
```
[1,1,2,2,3,3,5]
2
[1,2,3,4]
0
```

## Initial Template
```python
# Code template not available
```

## Solution
### Initial Thoughts

- **Problem Analysis**: The problem is to find the maximum number of prizes that can be won by optimally selecting two segments of length k on the x-axis. Each segment can collect prizes that fall within its range, and the segments can overlap.
- **Key Observations**:
   - The prizes are sorted in non-decreasing order, which means that they are arranged from left to right on the x-axis.
   - The length of each segment is k, which means that each segment can cover a range of k units on the x-axis.
   - The segments can overlap, which means that some prizes may be counted multiple times if they fall within the range of both segments.
- **Possible Approaches**:
   - **Brute Force**: Try all possible combinations of two segments of length k and count the number of prizes that each combination collects. The combination that collects the maximum number of prizes is the optimal solution. The time complexity of this approach is O(n^2), where n is the number of prizes.
   - **Two Pointers**: Use two pointers to iterate through the array of prizes. The first pointer represents the start of the first segment, and the second pointer represents the start of the second segment. Move the pointers forward until the length of the current segment is k, then count the number of prizes that fall within the current segment. Update the maximum number of prizes if the current segment collects more prizes than any previous segment. The time complexity of this approach is O(n), where n is the number of prizes.

### Solution Implementation
```python
def max_win(prizePositions, k):
    """
    :type prizePositions: List[int]
    :type k: int
    :rtype: int
    """
    # Initialize two pointers to the start of the array.
    left = 0
    right = 0
    
    # Initialize the maximum number of prizes to 0.
    max_prizes = 0
    
    # Iterate through the array of prizes.
    while right < len(prizePositions):
        # Calculate the length of the current segment.
        segment_length = prizePositions[right] - prizePositions[left] + 1
        
        # If the length of the current segment is less than k, move the right pointer forward.
        if segment_length < k:
            right += 1
        
        # If the length of the current segment is equal to k, count the number of prizes that fall within the current segment.
        elif segment_length == k:
            # Calculate the number of prizes that fall within the current segment.
            num_prizes = 0
            for i in range(left, right + 1):
                if prizePositions[i] >= prizePositions[left] and prizePositions[i] <= prizePositions[right]:
                    num_prizes += 1
            
            # Update the maximum number of prizes if the current segment collects more prizes than any previous segment.
            max_prizes = max(max_prizes, num_prizes)
            
            # Move both pointers forward.
            left += 1
            right += 1
        
        # If the length of the current segment is greater than k, move the left pointer forward.
        else:
            left += 1
    
    # Return the maximum number of prizes.
    return max_prizes
```

### Solution Explanation

The solution uses two pointers to iterate through the array of prizes. The first pointer represents the start of the first segment, and the second pointer represents the start of the second segment. The solution moves the pointers forward until the length of the current segment is k, then counts the number of prizes that fall within the current segment. The solution updates the maximum number of prizes if the current segment collects more prizes than any previous segment. The solution repeats this process until it reaches the end of the array of prizes.

The time complexity of the solution is O(n), where n is the number of prizes. The solution iterates through the array of prizes once, and each iteration takes O(1) time.

The space complexity of the solution is O(1), as it does not require any additional data structures.

### Complexity Analysis

- **Time Complexity**: O(n) - The solution iterates through the array of prizes once, and each iteration takes O(1) time.
- **Space Complexity**: O(1) - The solution does not require any additional data structures.

## Topics
Array, Binary Search, Sliding Window

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-14
