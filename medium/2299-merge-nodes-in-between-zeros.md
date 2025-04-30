# Merge Nodes in Between Zeros

## Problem Link
[LeetCode - Merge Nodes in Between Zeros](https://leetcode.com/problems/merge-nodes-in-between-zeros/)

## Difficulty
Medium

## Problem Description
<p>You are given the <code>head</code> of a linked list, which contains a series of integers <strong>separated</strong> by <code>0</code>&#39;s. The <strong>beginning</strong> and <strong>end</strong> of the linked list will have <code>Node.val == 0</code>.</p>

<p>For <strong>every </strong>two consecutive <code>0</code>&#39;s, <strong>merge</strong> all the nodes lying in between them into a single node whose value is the <strong>sum</strong> of all the merged nodes. The modified list should not contain any <code>0</code>&#39;s.</p>

<p>Return <em>the</em> <code>head</code> <em>of the modified linked list</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/02/02/ex1-1.png" style="width: 600px; height: 41px;" />
<pre>
<strong>Input:</strong> head = [0,3,1,0,4,5,2,0]
<strong>Output:</strong> [4,11]
<strong>Explanation:</strong> 
The above figure represents the given linked list. The modified list contains
- The sum of the nodes marked in green: 3 + 1 = 4.
- The sum of the nodes marked in red: 4 + 5 + 2 = 11.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/02/02/ex2-1.png" style="width: 600px; height: 41px;" />
<pre>
<strong>Input:</strong> head = [0,1,0,3,0,2,2,0]
<strong>Output:</strong> [1,3,4]
<strong>Explanation:</strong> 
The above figure represents the given linked list. The modified list contains
- The sum of the nodes marked in green: 1 = 1.
- The sum of the nodes marked in red: 3 = 3.
- The sum of the nodes marked in yellow: 2 + 2 = 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is in the range <code>[3, 2 * 10<sup>5</sup>]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 1000</code></li>
	<li>There are <strong>no</strong> two consecutive nodes with <code>Node.val == 0</code>.</li>
	<li>The <strong>beginning</strong> and <strong>end</strong> of the linked list have <code>Node.val == 0</code>.</li>
</ul>


## Test Cases
```
[0,3,1,0,4,5,2,0]
[0,1,0,3,0,2,2,0]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to merge nodes between zeros in a linked list.  The values between the zeros should be summed up and represented as a single node.
   - The list always starts and ends with a zero.  There are no consecutive zeros.
   - We can iterate through the linked list, keeping track of the sum between zeros. When we encounter a zero, we create a new node with the calculated sum and link it to the result list.

2. Solution Implementation:
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def mergeNodes(head: ListNode) -> ListNode:
    """Merges nodes between zeros in a linked list.

    Args:
        head: The head of the linked list.

    Returns:
        The head of the modified linked list.
    """

    dummy = ListNode(0)  # Dummy node to simplify linking
    tail = dummy 
    current = head.next  # Skip the initial zero
    current_sum = 0

    while current:
        if current.val == 0:  # Encountered a zero, create a new node with the sum
            new_node = ListNode(current_sum)
            tail.next = new_node
            tail = new_node
            current_sum = 0 # Reset the sum for the next group
        else:
            current_sum += current.val  # Accumulate the sum

        current = current.next

    return dummy.next # Return the linked list after the dummy node
```

3. Solution Explanation:
   - We use a dummy node `dummy` to simplify the process of building the new linked list. `tail` keeps track of the last node in the new list.
   - We iterate through the original list starting from the node after the initial zero.
   - Inside the loop, if the current node's value is 0, it indicates the end of a segment. We create a new node with the accumulated `current_sum` and append it to the new list. We then reset `current_sum` to 0.
   - If the current node's value is not 0, we add it to `current_sum`.
   - Finally, we return the linked list starting from the node after the dummy node.

4. Complexity Analysis:
   - Time complexity: O(N) - We traverse the linked list once. N is the number of nodes in the original list.
   - Space complexity: O(M) - We create a new linked list with M nodes, where M is the number of segments (number of zeros - 1).  In the worst-case scenario, where there's a 0 after every non-zero node, M could approach N/2.  So, the space complexity is proportional to the number of segments, which is at most N/2, simplifying to O(N). But on average, M will be much smaller than N.


## Topics
Linked List, Simulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-04-30
