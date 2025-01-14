# Min Stack

## Problem Link
[LeetCode - Min Stack](https://leetcode.com/problems/min-stack/)

## Difficulty
Medium

## Problem Description
<p>Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.</p>

<p>Implement the <code>MinStack</code> class:</p>

<ul>
	<li><code>MinStack()</code> initializes the stack object.</li>
	<li><code>void push(int val)</code> pushes the element <code>val</code> onto the stack.</li>
	<li><code>void pop()</code> removes the element on the top of the stack.</li>
	<li><code>int top()</code> gets the top element of the stack.</li>
	<li><code>int getMin()</code> retrieves the minimum element in the stack.</li>
</ul>

<p>You must implement a solution with <code>O(1)</code> time complexity for each function.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;MinStack&quot;,&quot;push&quot;,&quot;push&quot;,&quot;push&quot;,&quot;getMin&quot;,&quot;pop&quot;,&quot;top&quot;,&quot;getMin&quot;]
[[],[-2],[0],[-3],[],[],[],[]]

<strong>Output</strong>
[null,null,null,null,-3,null,0,-2]

<strong>Explanation</strong>
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>-2<sup>31</sup> &lt;= val &lt;= 2<sup>31</sup> - 1</code></li>
	<li>Methods <code>pop</code>, <code>top</code> and <code>getMin</code> operations will always be called on <strong>non-empty</strong> stacks.</li>
	<li>At most <code>3 * 10<sup>4</sup></code> calls will be made to <code>push</code>, <code>pop</code>, <code>top</code>, and <code>getMin</code>.</li>
</ul>


## Test Cases
```
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]
```

## Initial Template
```python
# Code template not available
```

## Solution
### Initial Thoughts

- **Problem analysis**: The problem requires us to implement a stack that can perform push, pop, top, and getMin operations in constant time. The key is to maintain a minimum value in the stack so that we can retrieve it efficiently.
- **Key observations**: Since the stack should support constant time operations, we need to avoid using a sorted list or a heap to track the minimum value.
- **Possible approaches**:
 - **Naive approach**: We can simply store the minimum value in a variable and update it whenever a smaller value is pushed onto the stack. However, this approach has O(n) time complexity for getMin operation.
 - **Optimized approach**: We can use an auxiliary stack to track the minimum values. Whenever a smaller value is pushed onto the stack, we push it onto the auxiliary stack as well. When we pop an element from the stack, we also pop it from the auxiliary stack. This approach ensures that the minimum value is always at the top of the auxiliary stack, and we can retrieve it in constant time.


### Solution Implementation

```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self) -> None:
        if self.stack[-1] == self.min_stack[-1]:
            self.min_stack.pop()
        self.stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]
```


### Solution Explanation

- We use two stacks: `stack` to store the elements of the stack and `min_stack` to track the minimum values.
- When we push an element onto the stack, we check if it is smaller than or equal to the minimum value at the top of the `min_stack`. If it is, we push it onto the `min_stack`.
- When we pop an element from the stack, we also pop it from the `min_stack` if it is the minimum value.
- The top element of the `min_stack` is always the minimum value in the stack.
- All operations run in O(1) time complexity, including `getMin`, because we only need to access the top elements of the stacks.


### Complexity Analysis

- **Time complexity**:
 - **Push**: O(1)
 - **Pop**: O(1)
 - **Top**: O(1)
 - **GetMin**: O(1)
- **Space complexity**: O(n), where n is the maximum number of elements in the stack.

## Topics
Stack, Design

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-14
