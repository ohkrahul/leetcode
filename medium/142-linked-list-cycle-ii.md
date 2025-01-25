# Linked List Cycle II

## Problem Link
[LeetCode - Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

## Difficulty
Medium

## Problem Description
<p>Given the <code>head</code> of a linked list, return <em>the node where the cycle begins. If there is no cycle, return </em><code>null</code>.</p>

<p>There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the <code>next</code> pointer. Internally, <code>pos</code> is used to denote the index of the node that tail&#39;s <code>next</code> pointer is connected to (<strong>0-indexed</strong>). It is <code>-1</code> if there is no cycle. <strong>Note that</strong> <code>pos</code> <strong>is not passed as a parameter</strong>.</p>

<p><strong>Do not modify</strong> the linked list.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png" style="height: 145px; width: 450px;" />
<pre>
<strong>Input:</strong> head = [3,2,0,-4], pos = 1
<strong>Output:</strong> tail connects to node index 1
<strong>Explanation:</strong> There is a cycle in the linked list, where tail connects to the second node.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png" style="height: 105px; width: 201px;" />
<pre>
<strong>Input:</strong> head = [1,2], pos = 0
<strong>Output:</strong> tail connects to node index 0
<strong>Explanation:</strong> There is a cycle in the linked list, where tail connects to the first node.
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png" style="height: 65px; width: 65px;" />
<pre>
<strong>Input:</strong> head = [1], pos = -1
<strong>Output:</strong> no cycle
<strong>Explanation:</strong> There is no cycle in the linked list.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of the nodes in the list is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
	<li><code>-10<sup>5</sup> &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
	<li><code>pos</code> is <code>-1</code> or a <strong>valid index</strong> in the linked-list.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Can you solve it using <code>O(1)</code> (i.e. constant) memory?</p>


## Test Cases
```
[3,2,0,-4]
1
[1,2]
0
[1]
-1
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**
   - This problem is a classic example of detecting cycles in a linked list.
   - To solve this problem, we can use the classic Floyd's Tortoise and Hare algorithm.
   - The algorithm works by maintaining two pointers: a slow pointer (tortoise) and a fast pointer (hare). 
     - The slow pointer moves one step at a time, while the fast pointer moves two steps at a time.
     - If there is a cycle in the linked list, the slow and fast pointers will eventually meet at the same node.

2. **Solution Implementation:**
```python
def detectCycle(head):
    if not head:
        return None

    # Initialize slow and fast pointers
    slow = head
    fast = head

    # Keep moving the slow and fast pointers until they meet or the fast pointer reaches the end of the linked list
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

        # If the slow and fast pointers meet, then there is a cycle in the linked list
        if slow == fast:
            return slow

    # If the fast pointer reaches the end of the linked list, then there is no cycle
    return None
```

3. **Solution Explanation:**
   - The algorithm works as follows:
     - If there is no cycle in the linked list, the fast pointer will eventually reach the end of the linked list and the algorithm will return `None`.
     - If there is a cycle in the linked list, the slow and fast pointers will eventually meet at the same node, which is the start of the cycle.
     - When the slow and fast pointers meet, we can return the slow pointer, which will be pointing to the start of the cycle.

4. **Complexity Analysis:**
   - **Time complexity:** The time complexity of the algorithm is O(n), where n is the number of nodes in the linked list. The algorithm iterates over the linked list once, and each iteration takes constant time.
   - **Space complexity:** The space complexity of the algorithm is O(1). The algorithm does not require any additional space beyond the space required for the two pointers.

## Topics
Hash Table, Linked List, Two Pointers

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-25
